# iSCSI SharedFS dynamic provisioner

| Image                            | Build Status                         |
|----------------------------------|--------------------------------------|
| **[iscsi-sharedfs-provisioner]** | ![iscsi-sharedfs-provisioner-status] |

[iscsi-sharedfs-provisioner]: iscsi-sharedfs-provisioner
[iscsi-sharedfs-provisioner-status]: https://img.shields.io/docker/build/kvaps/iscsi-sharedfs-provisioner.svg

Runs as deployment.

Waits until `PersistentVolumeClaims` will be created in Kubernetes.

Then creates new drives with needed parameters and announce them as `PersistentVolume` in Kubernetes.

## Usage

* Create service account and cluster role for your provisioner:

  ```bash
  kubectl apply -f https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi-sharedfs-provisioner/serviceaccount.yaml
  ```

* Download example yaml for deployment and update it for passthrough your filesystem to both containers.
  Check configuration variables section below.

  ```bash
  curl -o iscsi-sharedfs-provisioner.yaml -L https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi-sharedfs-provisioner/iscsi-sharedfs-provisioner.yaml
  vim iscsi-sharedfs-provisioner.yaml
  kubectl apply -f iscsi-sharedfs-provisioner.yaml
  ```

  *In this example we are presume that your filesystem is mounted on `/stor/sharedfs` on every node*

  *better to passthrough upper directory (`/stor`) with your filesystem mountpoint for make possible mountpoint chek*

  **WARNING**
  
  If you use kubernetes < 1.10 version, you need to enable `mountPropagation` in featuregates.

* Check storageclass options section below, then create new storage class with your filesystem:

  ```bash
  curl -o class.yaml -L https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi-sharedfs-provisioner/class.yaml
  vim class.yaml
  kubectl apply -f class.yaml
  ```

* Create example claim and example pod

  ```bash
  kubectl apply -f https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi-sharedfs-provisioner/claim.yaml
  kubectl apply -f https://raw.githubusercontent.com/kvaps/kube-iscsi-loop/master/iscsi-sharedfs-provisioner/test-pod.yaml
  ```

## Configuration variables

* **PROVISIONER_NAME** - Your provisioner identificator (default: `kvaps/sharedfs`)

## Storageclass options

* **iqn** - iqn for clients, it should be same like `IQN` variable for [iscsi-sharedfs-publisher](../iscsi-sharedfs-publisher) image (example: `iqn.2018-09.org.loopback.sharedfs`)
* **lun** - lun number, it should be same like `LUN` variable for [iscsi-sharedfs-publisher](../iscsi-sharedfs-publisher) image (default: `1`)
* **mmpUpdateInterval** - set interval for enable multimount protection for filesystem. (example: `5`)
* **mountpoint** - Mountpoint for your filesystem (example: `/stor/sharedfs`)
* **directory** - relative path for images storage directory (example `images`)
