---

copyright:
  years: 2021, 2022
lastupdated: "2022-08-10"

keywords: 

subcollection: hpc-slurm

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:table: .aria-labeledby="caption"}

# Deployment values
{: #deployment-values}

The following deployment values can be used to configure the {{site.data.keyword.slurm_short}} cluster instance on {{site.data.keyword.Bluemix_notm}}.

| Value | Description | Type | Is it required? | Default value |
| ----- | ----------- | ---- | --------------- | ------------ |
| `api_key` | This is the {{site.data.keyword.Bluemix_notm}} API key for the {{site.data.keyword.Bluemix_notm}} account where the {{site.data.keyword.slurm_short}} cluster needs to be deployed. For more information on how to create an API key, see [Managing user API keys](/docs/account?topic=account-userapikey). | String | Yes | None |
| `cluster_id` | Unique ID of the cluster used by {{site.data.keyword.slurm_short}} for configuration of resources. This must be up to 39 alphanumeric characters including the underscore (_), the hyphen (-), and the period (.). Other special characters and spaces are not allowed. Do not use the name of any host or user as the name of your cluster. You cannot change it after installation. | String | No | `SlurmCluster` |
| `cluster_prefix` | Prefix that is used to name the {{site.data.keyword.slurm_short}} cluster and {{site.data.keyword.Bluemix_notm}} resources that are provisioned to build the Slurm cluster instance. You cannot create more than one instance of the {{site.data.keyword.slurm_short}} cluster with the same name. Make sure that the name is unique. | String | No | `hpcc-slurm` |
| `image_name` | Name of the image that you want to use to create virtual server instances in your {{site.data.keyword.Bluemix_notm}} account to deploy as worker nodes in the {{site.data.keyword.slurm_short}} cluster. By default, the automation uses a stock operating system image. If you would like to include your application-specific binary files, follow the instructions in [Planning for custom images](/docs/vpc?topic=vpc-planning-custom-images) to create your own custom image and use that to build the {{site.data.keyword.slurm_short}} cluster through this offering. Note that use of your own custom image might require changes to the cloud-init scripts, and potentially other files, in the Terraform code repository if different post-provisioning actions or variables need to be implemented.| String | No | `ibm-ubuntu-20-04-minimal-amd64-2` |
| `login_node_instance_type` | Specifies the virtual server instance profile type to be used to create the login node for the {{site.data.keyword.slurm_short}} cluster. For choices on profile types, see [Instance profiles](/docs/vpc?topic=vpc-profiles). | String | No | bx2-2x8 |
| `management_node_count` | Total number of management and management candidate nodes. Enter a value in the range 1 - 3.| Number | No | 1 |
| `management_node_instance_type` | Specify the virtual server instance profile type to be used to create the management nodes for the {{site.data.keyword.slurm_short}} cluster. For choices on profile types, see [Instance profiles](/docs/vpc?topic=vpc-profiles). | String | No | bx2-4x16 |
| `resource_group` | Resource group name from your {{site.data.keyword.Bluemix_notm}} account where the VPC resources should be deployed. **Note:** Do not modify the "Default" value if you would like to use the auto scaling capability. For additional information on resource groups, see [Managing resource groups](/docs/account?topic=account-rgs). | String | No | "Default" |
| `ssh_allowed_ips` | Comma-separated list of IP addresses that can access the {{site.data.keyword.slurm_short}} instance through an SSH interface. The default value allows any IP address to access the cluster. | String | No | 0.0.0.0/0 |
| `ssh_key_name` | Comma-separated list of names of the SSH key that is configured in your {{site.data.keyword.Bluemix_notm}} account and is used to establish a connection to the {{site.data.keyword.slurm_short}} management node. Ensure that the SSH key is present in the same resource group and region where the cluster is being provisioned. If you do not have an SSH key in your {{site.data.keyword.Bluemix_notm}} account, create one by using the instructions that are given at [SSH keys](/docs/vpc?topic=vpc-ssh-keys). | String | Yes | None |
| `storage_node_instance_type` | Specify the virtual server instance profile type to be used to create the storage nodes for the {{site.data.keyword.slurm_short}} cluster. The storage nodes are the ones that would be used to create an NFS instance to manage the data for HPC workloads. For choices on profile types, see [Instance profiles](/docs/vpc?topic=vpc-profiles). | String | No | bx2-2x8 |
| `volume_capacity` | Size in GB for the block storage that would be used to build the NFS instance and would be available as a mount on the {{site.data.keyword.slurm_short}} management node. Enter a value in the range 10 - 16,000. | Number | No | 100 |
| `volume_iops` | Number to represent the IOPS configuration for block storage to be used for the NFS instance (valid only for `volume_profile=custom`, dependent on `volume_capacity`). Enter a value in the range 100 - 48,000. For possible options of IOPS, see [Custom IOPS profile](/docs/vpc?topic=vpc-block-storage-profiles#custom). | Number | No | 300 |
| `volume_profile` | Name of the block storage volume type to be used for NFS instance. For possible options, see [Block storage profiles](/docs/vpc?topic=vpc-block-storage-profiles). | String | No | `general_purpose` |
| `vpc_name` | Name of an existing VPC in which the cluster resources will be deployed. If no value is given, then a new VPC is provisioned for the cluster. | String | No | None |
| `vpn_enabled` | Set the value as true to deploy a VPN gateway for VPC in the cluster.| bool | No | false |
| `vpn_peer_address` | The peer public IP address to which the VPN is connected.| String | No | `_NOT_SET_`  |
| `vpn_peer_cidrs` | Comma-separated list of peer CIDRs (for example, 192.168.0.0/24) to which the VPN is connected.| String | No | `_NOT_SET_`  |
| `vpn_preshared_key` | The pre-shared key for the VPN. | String | No | `_NOT_SET_` |
| `worker_node_count` | This is the number of worker nodes that are provisioned at the time the cluster is created. Enter a value in the range 1 - 500. | Number | No | 1 |
| `worker_node_instance_type` | Specify the virtual server instance profile type to be used to create the worker nodes for the {{site.data.keyword.slurm_short}} cluster. The worker nodes are the ones where the workload execution takes place and the choice must be made according to the characteristics of the workloads. For choices on profile types, see [Instance profiles](/docs/vpc?topic=vpc-profiles). | String | No | bx2-4x16 |
| `zone` | {{site.data.keyword.Bluemix_notm}} zone name within the selected region where the {{site.data.keyword.slurm_short}} cluster must be deployed. To get a full list of zones within a region, see [Get zones by using the CLI](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region#get-zones-using-the-cli). | String | Yes | None |
{: caption="Deployment values" caption-side="top"} 
