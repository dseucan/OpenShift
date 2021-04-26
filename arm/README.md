# "arm" Directory
This directory contains sample ARM templates for creating private cluster virtual networks and subnets.
The address spaces were carefully designed so that they do not overlap, contain an appropriate number of IP address for the needs of each subnet, and do not consume excess IPv4 address space.

## Address spaces
There are 4 virtual networks creatable from these templates, each occupying a separate /18 address space:
- ulrik - 10.16.0.0/18
- vitek - 10.16.64.0/18
- witek - 10.16.128.0/18
- xacik - 10.16.196.0/18

Within each virtual network these templates create 5 subnets:
- pods - pool to automatically allocate pod IP addresses from
- services - pool to automatically allocate service IP addresses from
- masters - pool to automatically allocate master IP addresses from
- infras - pool to automatically allocate infra IP addresses from
- workers - pool to automatically allocate worker IP addresses from

It is important that all of the "machine" subnets (masters, infras, workers) are allocated within a CIDR (not crossing CIDR boundaries).
In the OpenShift installation file (`install-config.yaml`), the union of these subnets must be declared for the `metadata.machineNetwork` parameter.

For the networks given above, this is how the subnets are mapped out. Note that the entire set of 4 clusters maps directly into the 10.16.0.0/16 address space.

subnet | address space  | pods           | services       | machineNetwork | masters        | infras         | workers
-------|----------------|----------------|----------------|----------------|----------------|----------------|---------------
ulrik  | 10.16.0.0/18   | 10.16.0.0/19   | 10.16.32.0/20  | 10.16.48.0/20  | 10.16.48.0/22  | 10.16.52.0/22  | 10.16.56.0/21
vitek  | 10.16.64.0/18  | 10.16.64.0/19  | 10.16.96.0/20  | 10.16.112.0/20 | 10.16.112.0/22 | 10.16.116.0/22 | 10.16.120.0/21
witek  | 10.16.128.0/18 | 10.16.128.0/19 | 10.16.160.0/20 | 10.16.176.0/20 | 10.16.176.0/22 | 10.16.180.0/22 | 10.16.184.0/21
xacik  | 10.16.192.0/18 | 10.16.192.0/19 | 10.16.224.0/20 | 10.16.240.0/20 | 10.16.240.0/22 | 10.16.244.0/22 | 10.16.248.0/21

# ARM template
There are 6 files that compries the ARM template:
1. `vnet.tmpl.json` - the master template containing the templatized resource definitions.
2. `vnet.stdparam.json` - the standard parameters passed into the master template that are the same for each cluster
3. `vnet.*.param.json` - the individual per-cluster parameters passed into the master to create their virtual networks and subnets.

The main template and stdparam file should not have to be changed.
The individual cluster parameter files are pre-populated with the address space and subnet definitons shown above.

# Building a virtual network for a cluster
1. Create a resource group for the cluster networks:

    ```
    cluster=vitek
    location=eastus
    az group create --resource-group $cluster-rg --location $location
    ```
    
2. Deploy the template with cluster-specific and standard parameter files:

    ```
    az deployment group create --resource-group $cluster-rg --template-file vnet.tmpl.json \
      --parameters @vnet.stdparam.json --parameters @vnet.$cluster.param.json
    ```
      
    
