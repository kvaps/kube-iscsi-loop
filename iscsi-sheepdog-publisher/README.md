# iSCSI Sheepdog Publisher

| Image                    | Build Status                 |
|--------------------------|------------------------------|
| **[sheepdog-publisher]** | ![sheepdog-publisher-status] |

[sheepdog-publisher]: sheepdog-publisher
[sheepdog-publisher-status]: https://img.shields.io/docker/build/kvaps/sheepdog-publisher.svg

Runs as daemonset.

Periodically checks sheepdog cluster for newly created images and creates iSCSI targets
for local use only.

After that you can use built-in iSCSI driver in Kubernetes for connect your images into pods.

**WARNING**

Sheepdog is quite experimental storage, use it at your own risk.


## Usage

* Check configuration variables in bellow

* Use example yaml for deploy your own installation:

  ```bash
  curl -o iscsi-sheepdog-publisher.yaml -L https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi-sheepdog-publisher/iscsi-sheepdog-publisher.yaml
  vim iscsi-sheepdog-publisher.yaml
  kubectl apply -f iscsi-sheepdog-publisher.yaml
  ```
  
  *In this example we are presume that your filesystem is mounted on /stor/sheepdog on every node*

## Configuration variables

* **ADDRESS** - Sheepdog bind address (default: `127.0.0.1`)
* **PORT** - Sheepdog bind port (default: `7000`)
* **IQN** - IQN name prefix for new targets (example: `iqn.2018-09.org.loopback.sheepdog`)
* **TIMEOUT** - Timeout between checks (default: `10`)
* **LUN** - LUN for the each new image (default: `1`)
