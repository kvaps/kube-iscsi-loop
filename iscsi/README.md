# iSCSI Daemons

| Image       | Build Status    |
|-------------|-----------------|
| **[iscsi]** | ![iscsi-status] |

[iscsi]: iscsi
[iscsi-status]: https://img.shields.io/docker/build/kvaps/iscsi.svg

This image includes `tgtd` and `iscsid` daemons, both of them are necessary for allow
publishers announce images, and connect them to your pods.

Runs as daemonsets, but can be replaced by locally runned daemons.
