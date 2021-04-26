# "arm" Directory
This directory contains sample ARM templates for creating private cluster virtual networks and subnets.

There are 4 virtual networks creatable from these templates, each occupying a separate /18 address space:
- ulrik - 10.16.0.0/18
- vadik - 10.16.64.0/18
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
vadik  | 10.16.64.0/18  | 10.16.64.0/19  | 10.16.96.0/20  | 10.16.112.0/20 | 10.16.112.0/22 | 10.16.116.0/22 | 10.16.120.0/21
witek  | 10.16.128.0/18 | 10.16.128.0/19 | 10.16.160.0/20 | 10.16.176.0/20 | 10.16.176.0/22 | 10.16.180.0/22 | 10.16.184.0/21
xacik  | 10.16.196.0/18 | 10.16.196.0/19 | 10.16.224.0/20 | 10.16.240.0/20 | 10.16.240.0/22 | 10.16.244.0/22 | 10.16.248.0/21
