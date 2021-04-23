# "arm" Directory
This directory contains ARM templates for creating private cluster virtual networks and subnets.

There are 4 virtual networks creatable from these templates, each occupying a separate /18 address space:
- ulrik - 10.16.0.0/18
- vadik - 10.16.64.0/18
- witek - 10.16.128.0/18
- xacik - 10.16.196.0/18

Within each virtual network these templates create 5 subnets:
- pods
- service
- masters
- infras
- workers

It is important that all of the "machine" subnets (masters, infras, workers) 
