# kube-iscsi-loop

Loop iSCSI interfaces and daemons for K8S.

## Components

### Backend

The next backends supported

* **SharedFS** - images are simple files thats stores on some shared filesystem.

* **Sheepdog** - sheepdog images. Your nodes should be part of sheepdog cluster.</br> However you can use [containerized sheepdog](https://github.com/kvaps/kube-sheepdog).

### Frontend

Project uses built-in kubernetes **iSCSI** driver for connect drivers into pods.

## Limitations and Requirements

This implementation implies using locally runned iSCSI daemons with some
distributed shared filesystem as backend, this filesystem should be directly connected to all nodes.

It's not difficult to update those scripts for use with remote runned iSCSI-daemon
(take a look on sharedfs provisioners): you can add some authentication parameters, multipathing eg.,
and bind targets to `0.0.0.0` instead `127.0.0.1`.</br>
If you do this please send me your PR.

Otherwise you can simple use [iSCSI-targetd provisioner](https://github.com/kubernetes-incubator/external-storage/tree/master/iscsi/targetd)

## Images

### iSCSI Daemons

| Image       | Build Status    |
|-------------|-----------------|
| **[iscsi]** | ![iscsi-status] |

[iscsi]: iscsi
[iscsi-status]: https://img.shields.io/docker/build/kvaps/iscsi.svg

This image includes `tgtd` and `iscsid` daemons, both of them are necessary for allow
publishers announce images, and connect them to your pods.

Runs as daemonsets, but can be replaced by locally runned daemons.

### iSCSI Dynamic provisioners

| Image                            | Build Status                         |
|----------------------------------|--------------------------------------|
| **[iscsi-sharedfs-provisioner]** | ![iscsi-sharedfs-provisioner-status] |
| **[iscsi-sheepdog-provisioner]** | ![iscsi-sheepdog-provisioner-status] |

[iscsi-sharedfs-provisioner]: iscsi-sharedfs-provisioner
[iscsi-sheepdog-provisioner]: iscsi-sheepdog-provisioner
[iscsi-sharedfs-provisioner-status]: https://img.shields.io/docker/build/kvaps/iscsi-sharedfs-provisioner.svg
[iscsi-sheepdog-provisioner-status]: https://img.shields.io/docker/build/kvaps/iscsi-sheepdog-provisioner.svg

Runs as deployment.

Waits until `PersistentVolumeClaims` will be created in Kubernetes.

Then creates new drives with needed parameters and announce them as `PersistentVolume` in Kubernetes.

### iSCSI Publishers

| Image                          | Build Status                       |
|--------------------------------|------------------------------------|
| **[iscsi-sharedfs-publisher]** | ![iscsi-sharedfs-publisher-status] |
| **[iscsi-sheepdog-publisher]** | ![iscsi-sheepdog-publisher-status] |

[iscsi-sharedfs-publisher]: iscsi-sharedfs-publisher
[iscsi-sheepdog-publisher]: iscsi-sheepdog-publisher
[iscsi-sharedfs-publisher-status]: https://img.shields.io/docker/build/kvaps/iscsi-sharedfs-publisher.svg
[iscsi-sheepdog-publisher-status]: https://img.shields.io/docker/build/kvaps/iscsi-sheepdog-publisher.svg

Runs as daemonset.

Periodically checks some API for newly created images and creates iSCSI targets
for local use only.

After that you can use built-in iSCSI driver in Kubernetes for connect your images into pods.
