---

copyright:
  years: 2021, 2022
lastupdated: "2022-09-30"

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

# Updating variables with Schematics API
{: #update-variables}

1. To update variables by using the {{site.data.keyword.bplong}} Python APIs, create two Python files, and provide a name of your choice for those files, for example, `schematics_variables_update.py` and `schematics_env_class.py`.
2. Copy and paste the [`schematics_variables_update.py`](/docs/hpc-slurm?topic=hpc-slurm-update-variables#example-request-update-variables) and [`schematics_env_class.py`](/docs/hpc-slurm?topic=hpc-slurm-update-variables#example-request-update-variables-file) Python example code requests to the respective Python files.
3. Copy and paste the [`config.json` template file](/docs/hpc-slurm?topic=hpc-slurm-update-variables#template-file) to a JSON file, for example `config.json`.
4. Change the following parameters as part of the request:
    * Provide the `workspace ID w_id` generated in both the following functions: `schematic_obj.get_workspace(w_id="<w_id>)` and `schematic_obj.update_variables(w_id="<wi_id>")`.
5. Make sure to update the required parameters, such as `api_key`, `ssh_key_name`, `cluster_prefix` in the `config.json` file.
6. Run the Python script by using python3 to update the variables in the {{site.data.keyword.bpshort}} workspace in the {{site.data.keyword.cloud_notm}}.

The following parameters might not be required in `config.json` as the {{site.data.keyword.bpshort}} update variables API uses the `workspace ID w_id` to update the variables against that workspace.
{: note}

```
{
  "name": "Schematic Dev Workspace",
  "type": [
    "terraform_v0.14"
  ],
  "location": "us-south",
  "description": "Schematic Dev Workspace",
  "tags": [],
  "template_repo": {
    "url": "<GitHub repo URL>",
    "githubtoken": "<github-token>"
  }
```
{: screen}

## Example Python request for `schematics_variables_update.py` file
{: #example-request-update-variables}

The following Python example request is for the example file `schematics_variables_update.py`.

```python
import logging, os, json

logging.basicConfig()
logging.root.setLevel(logging.NOTSET)
logging.basicConfig(level=logging.NOTSET)

from schematics_env_class import HPCCEnvironmentValues

logging.info("Schematic Variable Update Started")

if __name__ == '__main__':

    json_files = os.path.join(os.path.abspath("."), "config.json")

    with open(json_files, "r") as file:
        config_data = json.load(file)

    api_key = config_data["template_data"][0]["variablestore"][1]["value"]

    schematic_obj = HPCCEnvironmentValues(api_key)

    workspace_response = schematic_obj.schematics_service.get_workspace(w_id="<workspace id>").get_result()
    schematic_obj.update_variables(w_id="<workspace id>", 
        t_id=workspace_response["template_data"][0]["id"], 
        variablestore=config_data["template_data"][0]["variablestore"]
    )

logging.info("Schematic Variable Update Completed")
```
{: codeblock}

## Example Python request for `schematics_env_class.py` file
{: #example-request-update-variables-file}

```python
import json
import logging

from ibm_cloud_sdk_core.authenticators import IAMAuthenticator
from ibm_schematics import SchematicsV1

class HPCCEnvironmentValues:

    def __init__(self, api_key):
        """
        create schematic services
        """
        self.authenticator = IAMAuthenticator(api_key)
        self.schematics_service = SchematicsV1(authenticator=self.authenticator)

        self.schematics_service.set_service_url('https://us.schematics.cloud.ibm.com')
        logging.info("Schematic Services created")

    def update_variables(self, w_id, t_id, variablestore):

        print("Function Schematic Update Variables Started")
        variables_update_result = self.schematics_service.replace_workspace_inputs(w_id=w_id, t_id=t_id, variablestore=variablestore
    ).get_result()

        return variables_update_result   
```
{: codeblock}

## `config.json` template file
{: #template-file}

Use this template file in the public GitHub repository: [config.json](https://github.com/IBM-Cloud/hpc-cluster-slurm/blob/main/sample/configs/hpc_workspace_config.json){: external}

## Example Python response
{: #example-python-response-update-variables}

```python
INFO:root:Variable Update started
INFO:root:Schematic Services created
DEBUG:urllib3.connectionpool:Starting new HTTPS connection (1): iam.cloud.ibm.com:443
DEBUG:urllib3.connectionpool:https://iam.cloud.ibm.com:443 "POST /identity/token HTTP/1.1" 200 1055
DEBUG:urllib3.connectionpool:Starting new HTTPS connection (1): us.schematics.cloud.ibm.com:443
DEBUG:urllib3.connectionpool:https://us.schematics.cloud.ibm.com:443 "GET /v1/workspaces/us-south.workspace.Sample-Schematics-Api-workspace.0f4b9089 HTTP/1.1" 200 None
Function Schematics Update Variables started
DEBUG:urllib3.connectionpool:https://us.schematics.cloud.ibm.com:443 "PUT /v1/workspaces/us-south.workspace.Sample-Schematics-Api-workspace.0f4b9089f/template_data/ad5540ad-d70d-40/values HTTP/1.1" 200 None
INFO:root:Variable Update Completed
```
{: screen}
