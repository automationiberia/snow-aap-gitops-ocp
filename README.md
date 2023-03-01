# GitOps-Demo

Repository to deploy Ansible Automation Platform (AAP) on Openshift (OCP). It will be deployed an instance of an Private Automation Hub (PAH) and an instance of an Automation Controller (former Ansible Tower) on already deployed Openshift infraestructure. The  OCP cluster is deployed in AWS and a shared filesystem is needed to deploy the PAH, which S3 is used in order to deploy it.

## Packages required

```
$  python3 -m pip install ansible-navigator --user
$  python3 -m pip install ansible-builder --user
```
## Populate your credentials and customer data

```
$ vim group_vars/all/main.yml
$ vim group_vars/all/vault
$ ansible-vault encrypt group_vars/all/vault
```
## Create OCP object needed to deploy AAP

```
$ ansible-navigator run bootstrap.yaml -i inventory -l cluster1 -m stdout --eei quay.io/automationiberia/ee-ocp-aap-iac-casc --vault-password-file .vault_password
$ ansible-navigator run bootstrap.yaml -i inventory -l cluster2 -m stdout --eei quay.io/automationiberia/ee-ocp-aap-iac-casc --vault-password-file .vault_password
```
## Variables


|Variable Name|Default Value|Required|Description|Example|
|:---|:---:|:---:|:---|:---|
|`ocp_api_key`|n/a|yes|Token used to authenticate with the Openshift API|'sha256~Po6ydC7CVs12drESQeNiUW9poUT84aFrj7zL3VQfvrS'|
|`ocp_api_host`|n/a|yes|Provide a URL for accessing the Openshift API|'=https://api.cluster-ocp.lab.example.com:6443'|
|`ocp_api_validate_certs`|false|no|Whether or not to verify the API server’s SSL certificates|'true'|
|`aws_access_key`|n/a|yes|Amazon Access Key to access AWS API|'R767AKIFYSF5INA6QKB6'|
|`aws_secret_key`|n/a|yes|Amazon Secret Key to access AWS API|'qKCYpd/jQX6gRhucQwIT1d2lzrapZ/O4lpEKGGqR'|
|`aws_region`|n/a|yes|Amazon region where the S3 will be deploy it|'us-central-3'|
|`s3_bucket_name`|"n/a"|yes|Name of the S3 bucket that will be created and used by PAH|'hub-demo-bucket'|
|`s3_bucket_secret_pah_name`|"n/a"|yes|Name of the secret that will be used by PAH to access the S3 bucket |'s3-secret-automationhub'|
|`aap_ocp_namespace`|n/a|ansible-automation-platform|Name of the namespace where the AAP will be deploy it|'ansible-automation-platform'|
