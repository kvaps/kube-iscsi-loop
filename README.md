# kube-iscsi-lb

Loopback iSCSI interfaces for k8s.

### iSCSI Daemons

| Image       | Build Status    |
|-------------|-----------------|
| **[iscsi]** | ![iscsi-status] |

[iscsi]: iscsi
[iscsi-status]: https://img.shields.io/docker/build/kvaps/iscsi.svg

This image includes `tgtd` and `iscsid` daemons, both of them are necessary for allow
publishers announce images, and connect them to your pods.

Runs as daemonsets, but can be replaced by locally runned daemons.

### iSCSI Publishers

| Image                    | Build Status                 |
|--------------------------|------------------------------|
| **[sharedfs-publisher]** | ![sharedfs-publisher-status] |
| **[sheepdog-publisher]** | ![sheepdog-publisher-status] |

[sharedfs-publisher]: sharedfs-publisher
[sheepdog-publisher]: sheepdog-publisher
[sharedfs-publisher-status]: https://img.shields.io/docker/build/kvaps/sharedfs-publisher.svg
[sheepdog-publisher-status]: https://img.shields.io/docker/build/kvaps/sheepdog-publisher.svg

Runs as daemonset.

Periodically checks some API for newly created images and creates iSCSI targets
for local use only.

After that you can use built-in iSCSI driver in Kubernetes for connect your images into pods.

### Dynamic provisioners

| Image                      | Build Status                   |
|----------------------------|--------------------------------|
| **[sharedfs-provisioner]** | ![sharedfs-provisioner-status] |
| **[sheepdog-provisioner]** | ![sheepdog-provisioner-status] |

[sharedfs-provisioner]: sharedfs-provisioner
[sheepdog-provisioner]: sheepdog-provisioner
[sharedfs-provisioner-status]: https://img.shields.io/docker/build/kvaps/sharedfs-provisioner.svg
[sheepdog-provisioner-status]: https://img.shields.io/docker/build/kvaps/sheepdog-provisioner.svg

Waits until `PersistentVolumeClaims` will be created in Kubernetes.

Then creates new drives with needed parameters and announce them as `PersistentVolume` in Kubernetes.
