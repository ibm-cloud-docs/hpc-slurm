---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-29"

keywords: 

subcollection: hpc-slurm

---

{:support: data-reuse='support'}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Troubleshooting
{: #troubleshooting-slurm}

## Why is IBM Cloud Schematics not able to clone the private GitHub repo?
{: #troubleshoot-topic-1}
{: troubleshoot}
{: support}

{{site.data.keyword.bpshort}} isn't able to clone the private GitHub repository, and you are seeing the following error message: `Failed to clone git repository, repository not found (check url, also check the scope 'repo' of the personal access token if SCHEMATICSGITTOKEN is used)`
{: tsSymptoms}

You didn't provide the correct GitHub token, or you didn't provide a GitHub token altogether.
{: tsCauses}

Provide a [GitHub token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token){: external} and check to see whether the correct GitHub token is provided in the `github_token` parameter in the created workspace API.
{: tsResolve}

## Why is IBM Cloud Schematics not able to clone the public GitHub repo?
{: #troubleshoot-topic-2}
{: troubleshoot}
{: support}

{{site.data.keyword.bpshort}} isn't able to clone the public GitHub repository, and you are seeing one of the following error messages:

* `Fatal, could not download repo, Failed to clone git repository, authentication required (or the git url is incorrect). Problems found with the Repository. Please Rectify and Retry`
* `Template error: Failed to clone git repository, authentication required (or the git url is incorrect)`
{: tsSymptoms}

You didn't provide the correct GitHub URL, or you provided a GitHub token, which is not required to clone a public repo. A GitHub access token is only required to access a private repo.
{: tsCauses}

Do not provide a GitHub token, and check to see whether the GitHub token was provided in the `github_token` parameter while creating a workspace by using the public repo.
{: tsResolve}

## Why is IBM Cloud Schematics not able to create a workspace?
{: #troubleshoot-topic-3}
{: troubleshoot}
{: support}

{{site.data.keyword.bpshort}} isn't able to create a workspace, and you are seeing the following error message: `You don't have the required to create a workspace in any resource groups. You must be assigned the manager role on the {{site.data.keyword.bpshort}} service in at least one resource group. Contact your account administrator for access.`
{: tsSymptoms}

You don't have the required access to create a workspace in any resource groups. You must be assigned the manager role on the {{site.data.keyword.bpshort}} service in at least one resource group.
{: tsCauses}

Contact your account administrator and get assigned with the manager role on the {{site.data.keyword.bpshort}} service in at least one resource group.
{: tsResolve}

## Why is IBM Cloud Schematics not able to provision the cluster and fails with an authorization error?
{: #troubleshoot-topic-5}
{: troubleshoot}
{: support}

{{site.data.keyword.bpshort}} isn't able to provision the cluster, and you are seeing the following error message: `Request is not authorized. Check your user permissions and authorizations and try again.`
{: tsSymptoms}

You don't have the required access to get any VPC resources provisioned. 
{: tsCauses}

Contact your account administrator and get all the required accesses. For more information, see [Required permissions](https://cloud.ibm.com/docs/vpc?topic=vpc-managing-user-permissions-for-vpc-resources&interface=cli).
{: tsResolve}

## Why is IBM Cloud Schematics not able to provision the cluster and fails with an error that the provided name is not unique? 
{: #troubleshoot-topic-6}
{: troubleshoot}
{: support}

{{site.data.keyword.bpshort}} isn't able to provision the cluster, and you are seeing the following example error message:
{: tsSymptoms}

```
"code": "validation_unique_failed",
"message": "Provided Name (sample-slurm-vpc) is not unique",
"target": {
"name": "name",
"type": "field",
"value": "sample-slurm-vpc"
}
```
{: screen}

VPC resource names must be unique. If a resource exists with the same name, you might get a similar error.
{: tsCauses}

Deprovision the existing resource and try again.
{: tsResolve}

## Why is IBM Cloud Schematics not able to provision the cluster while using a custom image?
{: #troubleshoot-topic-7}
{: troubleshoot}
{: support}

While using a custom image, {{site.data.keyword.bpshort}} isn't able to provision the cluster, and you are seeing one of the following error messages:

* `The arugment "image" is required, but no definition was found.`
* `Unknown variable. There is no variable named "image_id".`
{: tsSymptoms}

The custom image that is used for one of the virtual server instances isn't present in the target region and zone or it is not accessible by the account and API key that is used to provision the cluster.
{: tsCauses}

If you are using a custom image for any of your virtual server instances, ensure that the custom image is available in the target region and zone and is accessible by the account and API key that is used to provision the cluster.
{: tsResolve}

## Why am I receiving an error for the refresh token?
{: #troubleshoot-topic-8}
{: troubleshoot}
{: support}

You are receiving a refresh token error in the **generate a plan**, **apply a plan**, and **destroy resources** requests: `Error: The provided Refresh Token is invalid. Please provide a proper refresh token for Terraform to run the configuration. Code: 400`
{: tsSymptoms}

You didn't provide the correct refresh token, or you didn't provide a refresh token altogether.
{: tsCauses}

Check to see whether the refresh token that was generated by using the curl command is correct; otherwise, regenerate the refresh token.
{: tsResolve}

## Why am I receiving an error when I apply a change to my workspace?
{: #troubleshoot-topic-9}
{: troubleshoot}
{: support}

You are receiving the following error when you try to apply a change to your workspace: `Apply failed due to "Error: Error Deleting Volume : The volume is still attached to an instance."`
{: tsSymptoms}

After reconfiguring the volume profile, capacity, or IOPS, your workspace needs to be cleaned up before applying the change. 
{: tsCauses}

You need to destroy your existing resources and try applying the change again. Your data on the storage node is deleted if you destroy your existing resources.
{: tsResolve}
