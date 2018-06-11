# iSCSI SharedFS Publisher

| Image                    | Build Status                 |
|--------------------------|------------------------------|
| **[sharedfs-publisher]** | ![sharedfs-publisher-status] |

[sharedfs-publisher]: sharedfs-publisher
[sharedfs-publisher-status]: https://img.shields.io/docker/build/kvaps/sharedfs-publisher.svg

Runs as daemonset.

Periodically checks filesystem for newly created images and creates iSCSI targets
for local use only.

After that you can use built-in iSCSI driver in Kubernetes for connect your images into pods.

Your images should have `.img` extension

## Usage

* Check configuration variables in bellow

* Use example yaml for deploy your own installation:

  ```bash
  curl -o iscsi-sharedfs-publisher.yaml -L https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi-sharedfs-publisher/iscsi-sharedfs-publisher.yaml
  vim iscsi-sharedfs-publisher.yaml
  kubectl apply -f iscsi-sharedfs-publisher.yaml
  ```

  *In this example we are presume that your filesystem is mounted on /stor/sharedfs on every node*

**WARNING**

If you use kubernetes < 1.10 version, you need to enable `mountPropagation` in featuregates.


## Configuration variables

* **DIRECTORY** - Directory where publusher will check images (example: `/stor/sharedfs/images`)

  *this directory should be also visible for tgtd daemon by same path*
  
* **IQN** - IQN name prefix for new targets (example: `iqn.2018-09.org.loopback.sharedfs`)
* **TIMEOUT** - Timeout between checks (default: `10`)
* **LUN** - LUN for the each new image (default: `1`)
