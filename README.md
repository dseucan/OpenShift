# az-ocp-cluster
This project contains various utilties and templates for consistently creating OpenShift private clusters within 
an adequatly provoisioned Azure resource group, virtual networks, and their component subnets.

* [`arm`](arm/) - contains Azure Resource Manager templates for creating virtual networks and subnets
* [`bin`](bin/) - contains miscellaneous utilities useful for manipulating JSON and YAML
* [`misc`](misc/) - contains Linux environment setup advice for configuring an Azure and OCP administration controller machine
* [`templates`](templates/) - contains usable public and private cluster installation specifications for the `openshift-install` installer
