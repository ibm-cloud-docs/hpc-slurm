---

copyright:
  years: 2021
lastupdated: "2021-12-15"

keywords: 

subcollection: hpc-slurm

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:tip: .tip}
{:note .note}
{:important: .important}
{:table: .aria-labeledby="caption"}

# Deployment values
{: #deployment-values}

The following deployment values can be used to configure the Slurm cluster instance on IBM Cloud.

| Value | Description | Type | Is it required? | Default value |
| ----- | ----------- | ---- | --------------- | ------------ |
| `ssh_key_name` | Comma-separated list of names of the SSH key that is configured in your IBM Cloud account and is used to establish a connection to the Slurm master node. Ensure that the SSH key is present in the same resource group and region where the cluster is being provisioned. If you do not have an SSH key in your IBM Cloud account, create one by using the instructions given at [SSH keys](/docs/vpc?topic=vpc-ssh-keys). | string | Yes | n/a |
| `api_key` | This is the IBM Cloud API key for the IBM Cloud account where the Slurm cluster needs to be deployed. For more information on how to create an API key, see [Managing user API keys](/docs/account?topic=account-userapikey). | string | Yes | n/a |
| `vpc_name` | Name of an existing VPC in which the cluster resources will be deployed. If no value is given, then a new VPC will be provisioned for the cluster. Learn more. | string | Yes | None |
| `resource_group` | Resource group name from your IBM Cloud account where the VPC resources should be deployed. **Note:** Do not modify the "Default" value if you would like to use the auto-scaling capability. For additional information on resource groups, see [Managing resource groups](/docs/account?topic=account-rgs). | string | No | "Default" |
| `cluster_prefix` | Prefix that is used to name the Slurm cluster and IBM Cloud resources that are provisioned to build the Slurm cluster instance. You cannot create more than one instance of the Slurm cluster with the same name. Make sure that the name is unique. | string | No | `hpcc-slurm` |
| `cluster_id` | Unique ID of the cluster used by Slurm for configuration of resources. This must be up to 39 alphanumeric characters including the underscore (_), the hyphen (-), and the period (.). Other special characters and spaces are not allowed. Do not use the name of any host or user as the name of your cluster. You cannot change it after installation. | string | no | `SlurmCluster` |
| `zone` | IBM Cloud zone name within the selected region where the Slurm cluster should be deployed. To get a full list of zones within a region, see [Get zones by using the CLI](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region#get-zones-using-the-cli). | string | no | `us-south-3` |
| `image_name` | Name of the image that you want to use to create virtual server instances in your IBM Cloud account to deploy as worker nodes in the Slurm cluster. By default, the automation uses a stock operating system image. If you would like to include your application-specific binary files, follow the instructions in [Planning for custom images](https://cloud.ibm.com/docs/vpc?topic=vpc-planning-custom-images) to create your own custom image and use that to build the Slurm cluster through this offering. Note that use of your own custom image may require changes to the cloud-init scripts, and potentially other files, in the Terraform code repository if different post-provisioning actions or variables need to be implemented.| string | no | `ibm-ubuntu-20-04-minimal-amd64-2` |
| `management_node_instance_type` | Specify the virtual server instance profile type to be used to create the management nodes for the Slurm cluster. For choices on profile types, see [Instance profiles](/docs/vpc?topic=vpc-profiles). | String | no | bx2-4x16 |
| `worker_node_instance_type` | Specify the virtual server instance profile type to be used to create the worker nodes for the Slurm cluster. The worker nodes are the ones where the workload execution takes place and the choice should be made according to the characteristics of the workloads. For choices on profile types, see [Instance profiles](/docs/vpc?topic=vpc-profiles). | string | no | bx2-4x16 |
| `login_node_instance_type` | Specifies the virtual server instance profile type to be used to create the login node for the Slurm cluster. For choices on profile types, see [Instance profiles](/docs/vpc?topic=vpc-profiles). | string | no | bx2-2x8 |
| `storage_node_instance_type` | Specify the virtual server instance profile type to be used to create the storage nodes for the Slurm cluster. The storage nodes are the ones that would be used to create an NFS instance to manage the data for HPC workloads. For choices on profile types, see [Instance profiles](/docs/vpc?topic=vpc-profiles). | string | no | bx2-2x8 |
| `worker_node_count` | This is the number of worker nodes that will be provisioned at the time the cluster is created. Enter a value in the range 1 - 500. | number | no | 1 |
| `volume_capacity` | Size in GB for the block storage that would be used to build the NFS instance and would be available as a mount on the Slurm master node. Enter a value in the range 10 - 16,000. | number | no | 100 |
| `volume_iops` | Number to represent the IOPS configuration for block storage to be used for the NFS instance (valid only for `volume_profile=custom`, dependent on `volume_capacity`). Enter a value in the range 100 - 48,000. For possible options of IOPS, see [Custom IOPS profile](/docs/vpc?topic=vpc-block-storage-profiles#custom). | number | no | 300 |
| `management_node_count` | Total number of master and master candidate nodes. Enter a value in the range 1 - 3.| number | no | 1 |
| `ssh_allowed_ips` | Comma-separated list of IP addresses that can access the Slurm instance through an SSH interface. The default value allows any IP address to access the cluster. | string | no | 0.0.0.0/0 |
| `volume_profile` | Name of the block storage volume type to be used for NFS instance. For possible options, see [Block storage profiles](/docs/vpc?topic=vpc-block-storage-profiles). | string | no | `general_purpose` |
| `hyperthreading_enabled` | Setting this to true will enable hyper-threading in the worker nodes of the cluster (default). Otherwise, hyper-threading will be disabled. | bool | no | true |
| `vpn_enabled` |  Set the value as true to deploy a VPN gateway for VPC in the cluster.| bool | no | false |
| `vpn_peer_address` |  The peer public IP address to which the VPN will be connected.| string | no | `_NOT_SET_`  |
| `vpn_peer_cidrs` |  Comma separated list of peer CIDRs (e.g., 192.168.0.0/24) to which the VPN will be connected.| string | no | `_NOT_SET_`  |
| `vpn_preshared_key` |  The pre-shared key for the VPN| string | no | `_NOT_SET_`  |


