# Cluster add-ons

## Overview

Cluster add-ons are resources like Services and Deployments (with pods) that are
shipped with the Kubernetes binaries and are considered an inherent part of the
Kubernetes clusters.

There are currently two classes of add-ons:
- Add-ons that will be reconciled.
- Add-ons that will be created if they don't exist.

More details could be found in [addon-manager/README.md](addon-manager/README.md).

## Cooperating Horizontal / Vertical Auto-Scaling with "reconcile class addons"

"Reconcile" class addons will be periodically reconciled to the original state given
by the initial config. In order to make Horizontal / Vertical Auto-scaling functional,
the related fields in config should be left unset. More specifically, leave `replicas`
in `ReplicationController` / `Deployment` / `ReplicaSet` unset for Horizontal Scaling,
leave `resources` for container unset for Vertical Scaling. The periodic reconcile
won't clobbered these fields, hence they could be managed by Horizontal / Vertical
Auto-scaler.

## Add-on naming

The suggested naming for most of the resources is `<basename>` (with no version number).
Though resources like `Pod`, `ReplicationController` and `DaemonSet` are exceptional.
It would be hard to update `Pod` because many fields in `Pod` are immutable. For
`ReplicationController` and `DaemonSet`, in-place update may not trigger the underlying
pods to be re-created. You probably need to change their names during update to trigger
a complete deletion and creation.

## Acknowledgement
Forked from [kubernetes/kubernetes](https://github.com/kubernetes/kubernetes/tree/v1.8.2/cluster/addons) and periodically updated.

## Support
We use Slack for public discussions. To chit chat with us or the rest of the community, join us in the [Kubernetes Slack team](https://kubernetes.slack.com/messages/C81LSKMPE/details/) channel `#pharmer`. To sign up, use our [Slack inviter](http://slack.kubernetes.io/).

To receive product announcements, please join our [mailing list](https://groups.google.com/forum/#!forum/pharmer) or follow us on [Twitter](https://twitter.com/AppsCodeHQ). Our mailing list is also used to share design docs shared via Google docs.

If you have found a bug with Pharmer or want to request for new features, please [file an issue](https://github.com/pharmer/pharmer/issues/new).
