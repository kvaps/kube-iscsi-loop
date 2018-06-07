# Sharedfs iSCSI Publisher

| Image                    | Build Status                 |
|--------------------------|------------------------------|
| **[sharedfs-publisher]** | ![sharedfs-publisher-status] |

[sharedfs-publisher]: sharedfs-publisher
[sharedfs-publisher-status]: https://img.shields.io/docker/build/kvaps/sharedfs-publisher.svg

Runs as daemonset.

Periodically checks filesystem for newly created images and creates iSCSI targets
for local use only.

After that you can use built-in iSCSI driver in Kubernetes for connect your images into pods.

## Configuration variables

* **DIRECTORY** - Directory where publusher will check images (example: `/images`)

  *this directory should be also visible for tgtd daemon by same path*
  
* **IQN** - IQN name prefix for new targets (example: `iqn.2018.09.org.loopback.sharedfs`)
* **TIMEOUT** - Timeout between checks (default: `10`)
* **LUN** - LUN for the each new image (default: `1`)
