# iSCSI Sheepdog dynamic provisioner

| Image                            | Build Status                         |
|----------------------------------|--------------------------------------|
| **[iscsi-sheepdog-provisioner]** | ![iscsi-sheepdog-provisioner-status] |

[iscsi-sheepdog-provisioner]: iscsi-sheepdog-provisioner
[iscsi-sheepdog-provisioner-status]: https://img.shields.io/docker/build/kvaps/iscsi-sheepdog-provisioner.svg

Runs as deployment.

Waits until `PersistentVolumeClaims` will be created in Kubernetes.

Then creates new drives with needed parameters and announce them as `PersistentVolume` in Kubernetes.

**WARNING**

Sheepdog is quite experimental storage, use it at your own risk.

## Usage

* Create service account and cluster role for your provisioner:

  ```bash
  kubectl apply -f https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi-sheepdog-provisioner/serviceaccount.yaml
  ```

* Create sheepdog provisioner daemonset:

  ```bash
  kubectl apply -f https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi-sheepdog-provisioner/iscsi-sheepdog-provisioner.yaml
  ```

* Check storageclass options section below, then create new storage class with your filesystem:

  ```bash
  curl -o class.yaml -L https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi-sheepdog-provisioner/class.yaml
  vim class.yaml
  kubectl apply -f class.yaml
  ```

* Create example claim and example pod

  ```bash
  kubectl apply -f https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi-sheepdog-provisioner/claim.yaml
  kubectl apply -f https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi-sheepdog-provisioner/test-pod.yaml
  ```

## Configuration variables

* **PROVISIONER_NAME** - Your provisioner identificator (default: `kvaps/sheepdog`)

## Storageclass options

* **iqn** - iqn for clients, it should be same like `IQN` variable for [iscsi-sheepdog-publisher](../iscsi-sheepdog-publisher) image (example: `iqn.2018-09.org.loopback.sheepdog`)
* **lun** - lun number, it should be same like `LUN` variable for [iscsi-sheepdog-publisher](../iscsi-sheepdog-publisher) image (default: `1`)
* **address** - sheepdog bind address (default: `127.0.0.1`)
* **port** - sheepdog bind port (default: `7000`)
* **copies** - number of replaces (default: *as your cluster set*)
* **prealloc** - preallocate drive (default: `false`)
* **hyper** - create hyper volume (default: `false`)
* **block_size_shift** - set block size shift (default: *as your cluster set*)
