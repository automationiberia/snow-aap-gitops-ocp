# Service Now Objects Creation

Three playbooks are provided to create the following objects:

* Rest Message
  * OAuth authentication profile
  * POST HTTP Method
    * Variable Substitutions
* Workflow
  * Workflow Activity
  * Workflow Conditions and Transitions
* Standard Change Catalog Item
  * Variable Sets with the input Vars
  * Process Engine to run the previous Workflow

These playbooks must be executed in the numbered order:

1. 1_snow_rest_message.yaml
2. 2_snow_workflow.yaml
3. 3_snow_service_catalog.yaml

After executing the first playbook, the REST Message object will be created or updated. As a result of this, the operation `Get OAuth Token` must be manually performed to let the REST Message to work properly:

![ServiceNow Get OAuth Token](images/../../images/SNowGetOAuthToken.png)

