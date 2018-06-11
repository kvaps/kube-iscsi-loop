# iSCSI Daemons

| Image       | Build Status    |
|-------------|-----------------|
| **[iscsi]** | ![iscsi-status] |

[iscsi]: iscsi
[iscsi-status]: https://img.shields.io/docker/build/kvaps/iscsi.svg

This image includes `tgtd` and `iscsid` daemons, both of them are necessary for allow
publishers announce images, and connect them to your pods.

Runs as daemonsets, but can be replaced by locally runned daemons.

## Usage

If you going to use [iscsi-sharedfs-provisioner](../iscsi-sharedfs-provisioner) and
[iscsi-sharedfs-publisher](../iscsi-sharedfs-publisher), uncoment `/stor` mountpoint and write
your storage mountpoint instead.

**WARNING**

If you use kubernetes < 1.10 version, you need to enable `mountPropagation` in featuregates.

**Just run example yaml:**

```bash
kubectl apply -f https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi/iscsi.yaml
```
