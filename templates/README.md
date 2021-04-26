# "templates" Directory
This directory contains `openshift-install` templates that were used to create various clusters.

* `acluster.install-config.yaml` - this is the installation spec that was actually used to install the `acluster` public cluster.
* `bruce.install-config.yaml` - this is the installation spec that was actually used to install the `bruce` public cluster.
* `orig.install-config.yaml` - this is an unconfgured public cluster installation spec.
* `ulrik.install-config.yaml` - this is the installation spec that was acutally used to install the `ulrik` private cluster.
* `vitek.install-config.yaml` - this is a sample (working) installation spec that installs a second private cluster.

The clusters `ulrik` and `vitek` are configured consistently with the ARM templates provided in [`../arm` directory](../arm).
