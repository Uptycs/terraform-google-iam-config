# terraform gcp iam module 

This module allows you to create gcp credential config in Google Cloud Platform projects which will be used get gcp data from aws environment. 

This terraforms module will create below resources:-
 * It creates service account , workpool identity and add cloud provider to it .
 * It will attach below policies to service account 
     * roles/iam.securityReviewer 
     * roles/bigquery.resourceViewer
     * roles/pubsub.subscriber
     * roles/viewer

# Compatibility

This module is meant for use with Terraform version = "~> 3.61.0". If you haven't upgraded do terraform upgrade .


# Usage

## Install terraform (One-time)

## Get authentication
```
Option 1: Set credntial file in main.tf. Edit following line with credential file path
  - "credentials = file("CREDENTIALS_FILE.json")"
Option 2: Login with ADC
  - "gcloud auth application-default login"
```



# Modify locals.tf file as per requirement .
# 1. Pass GCP Project Details .
# 2. Pass Region and Zone
# 3. Set service account details
     # Set is_service_account_exists = true if service account is already exists and pass service account name in service_account_name .
     # Set is_service_account_exists = false if service account is not exists and give a new name to create service account in service_account_name.
# 4. Set Uptycs Cloudquery Host AWS account ID and AWS Role Name


#Execute Terraform Script to get credentials JSON
#Init
#  terraform init

#Plan and Verify
#  terraform plan

#Deploy the stack
#  terraform apply

#Note : Once terraform successfully applied then it will create "credentials.json" file on current path.

#Destroy
#  "terraform destroy"



# Remember :-
# 1. Workload Identity Pool can't be deleted permanently , It is soft-deleted , Soft-deleted providers are permanently deleted after approximately 30 days.
     You can restore a soft-deleted provider using UndeleteWorkloadIdentityPoolProvider. You cannot reuse the ID of a soft-deleted provider until it is permanently deleted.
     After terraform destroy same WIP can't be created again , So modify "WORKLOAD_IDENTITY" value if required.

# 2. credentials.json only create once until there are no changes on variables , for creating again same cred config json data ,please use command return by "Create_Credential_Config_file_command"