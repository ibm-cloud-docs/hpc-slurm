---

copyright:
  years: 2021, 2022
lastupdated: "2022-02-09"

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
{:faq: data-hd-content-type='faq'}

# FAQs
{: #slurm-faqs}

## What Slurm version is used in cluster nodes deployed with this offering?

{: #my-faq-packages}
{: faq}

Cluster nodes deployed with this offering include {{site.data.keyword.slurm_short}} 19.05.5-1 Advanced Edition. 

## What locations are available for deploying VPC resources?
{: #locations-vpc-resources}
{: faq}

Available regions and zones for deploying VPC resources, and a mapping of those to city locations and data centers can be found in [Locations for resource deployment](/docs/overview?topic=overview-locations){: external}.

## What permissions do I need in order to create a cluster using the offering?
{: #permissions-cluster-offering}
{: faq}

Instructions for setting the appropriate permissions for {{site.data.keyword.Bluemix_notm}} services that are used by the offering to create a cluster can be found in [Granting user permissions for VPC resources, Managing user access for Schematics, Assigning access to Secrets Manager](/docs/vpc?topic=vpc-managing-user-permissions-for-vpc-resources&locale=en).


## How do I SSH among nodes?
{: #ssh-among-nodes}
{: faq}

All of the nodes in the HPC cluster have the same public key that you register at your cluster creation. You can use ssh-agent forwarding, which is a common technique to access remote nodes that have the same public key. It automates to securely forward private keys to remote nodes. Forwarded keys are deleted immediately after a session is closed.

To securely forward private keys to remote nodes, you need to do `ssh-add` and `ssh -A`.

```
[your local PC]~$ ssh-add {id_rsa for slurm cluster}
[your local PC]~# ssh -A -J root@jumpbox_fip root@master_private_ip
...
[root@master]~# ssh -A worker_private_ip
```
{: codeblock}

For Mac OS X, you can persist `ssh-add` by adding the following configuration to `.ssh/config`:

```
Host *
  UseKeychain yes
  AddKeysToAgent yes
```
{: codeblock}

You can even remove `-A` by adding "ForwardAgent yes" to `.ssh/config`.

## How many worker nodes can I deploy in my Slurm cluster through this offering?
{: #worker-nodes}
{: faq}

Prior to deploying a cluster, it is important to ensure that the VPC resource quota settings are appropriate for the size of the cluster that you would like to create (see [Quotas and service limits](/docs/vpc?topic=vpc-quotas)).

The number of worker nodes that are supported for the deployment value worker_node_count is 500 (see [Deployment values](/docs/hpc-slurm?topic=hpc-slurm-deployment-values))). The worker_node_count variable specifies the number of worker nodes that are provisioned at the time that the cluster is created, which will exist throughout the life of the cluster.

When creating or deleting a cluster with a large number of worker nodes, you may encounter VPC resource provisioning or deletion failures. In those cases, running the {{site.data.keyword.bpshort}} apply or destroy operation again may result in the remaining resources being successfully provisioned or deleted. If you continue to see errors, see [Getting help and support](/docs/hpc-slurm?topic=hpc-slurm-getting-help-and-support).

## Does the offering support the Terraform parallelism flag?
{: #terraform-parallelism}
{: faq}

The Terraform [parallelism](https://www.terraform.io/docs/cloud/workspaces/variables.html#parallelism) flag is used to control the number of concurrent operations allowed for terraform plan, terraform apply, and terraform destroy. A larger number can result in faster overall cluster create and destroy times. However, too large a value may result in operation failures. For plan and apply, we recommend using values up to 250, and for destroy, we recommend using values up to 100. Note that setting the values for parallelism is not possible when using the [Schematics UI](https://test.cloud.ibm.com/docs/hpc-slurm?topic=hpc-slurm-creating-workspace&interface=ui). However, the values for that flag can be set in the config.json file used when creating the [Schematics workspace](https://test.cloud.ibm.com/docs/hpc-slurm?topic=hpc-slurm-creating-workspace&interface=cli#create-workspace-cli) via the CLI:

 ```
 "env_values":[
  { 
    "TF_CLI_ARGS_apply": "-parallelism=250"
  },
  { 
    "TF_CLI_ARGS_plan": "-parallelism=250"
  },
  {
    "TF_CLI_ARGS_destroy": "-parallelism=100"
  }]
  ```

## Why is "Default" not working as the value for resource_group?
{:defaut-not-working}
{: faq}

If you find that the "Default" value for `resource_group` does not work for you, check the Resource groups setting on your account to determine what the actual name of the default resource group is. For instance, it may be "default" instead.