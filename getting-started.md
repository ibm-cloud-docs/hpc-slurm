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
{:note: .note}
{:important: .important}
{:step: data-tutorial-type='step'}
{:table: .aria-labeledby="caption"}

# Getting started with Slurm
{: #getting-started-tutorial}

{{site.data.keyword.slurm_full_notm}} enables customers to deploy HPC clusters on {{site.data.keyword.Bluemix_notm}} infrastructure that use the [Slurm Workload Manager](https://github.com/SchedMD/slurm){: external} as a scheduling software. The deployment is performed by using Terraform and {{site.data.keyword.bplong_notm}} as automation frameworks. The following steps outline the high-level flow of events that are performed:

1. **Create a workspace** with the Terraform code from {{site.data.keyword.bplong_notm}}. This step defines the set of configuration properties that are used to perform the automation.
2. **Generate a plan** to confirm whether the configuration properties are valid, so that when you run the Terraform code, all of the resources are provisioned correctly. If the validation fails, fix the configuration properties and try again.
3. **Apply a plan** triggers the actual deployment of the {{site.data.keyword.cloud_notm}} resources to have an HPC cluster up and running by the time the deployment completes. If the deployment fails, identify the reason for failure, fix the problem, and try again. If a change is needed to the configuration properties, it might be better to generate a plan again.

Before you can deploy your {{site.data.keyword.slurm_short}} cluster, you need to create or gather some information. To get started, complete the following steps.

## Generate API key
{: #generate-api-key}
{: step}

Generate an API key for your {{site.data.keyword.cloud_notm}} account where the {{site.data.keyword.slurm_short}} cluster will be deployed. For more information, see [Managing user API keys](/docs/account?topic=account-userapikey).

## Create SSH key
{: #create-ssh-key}
{: step}

Create an SHH key in your {{site.data.keyword.cloud_notm}} account. This is your SSH key that you will use to access the Slurm cluster. For more information, see [Managing SSH keys](/docs/vpc?topic=vpc-managing-ssh-keys).

## Next steps
{: #getting-started-next-steps}
{: step}

After you've gathered the necessary input values to define your cluster configuration, you are ready to deploy your {{site.data.keyword.slurm_short}} cluster. The {{site.data.keyword.slurm_short}} cluster can be deployed on {{site.data.keyword.cloud_notm}} by using the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.bpshort}} UI, {{site.data.keyword.bpshort}} CLI, or the {{site.data.keyword.bpshort}} APIs. If you want to deploy your cluster by using the CLI or API, review the prerequisites for your interface of choice:

* [Setting up the {{site.data.keyword.bplong_notm}} CLI](/docs/hpc-slurm?topic=hpc-slurm-setting-up-cli)
* [Setting up the {{site.data.keyword.bplong_notm}} API](/docs/hpc-slurm?topic=hpc-slurm-setting-up-api)

After you've created and gathered your information and reviewed any additional prerequisites for your interface of choice, you are ready to begin [Creating a workspace](/docs/hpc-slurm?topic=hpc-slurm-creating-workspace).