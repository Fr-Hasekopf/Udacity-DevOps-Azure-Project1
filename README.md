# Azure Infrastructure Operations Project: Deploying a scalable IaaS web server in Azure

### Introduction
For this project, we will write a Packer template and a Terraform template to deploy a customizable, scalable web server in Azure.


### Dependencies
1. Create an [Azure Account](https://portal.azure.com) 
2. Install the [Azure command line interface](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
3. Install [Packer](https://www.packer.io/downloads)
4. Install [Terraform](https://www.terraform.io/downloads.html)

### Instructions
#### Clone this repo
git clone https://github.com/udacity/nd082-Azure-Cloud-DevOps-Starter-Code.git
 
##### Login to Azure CLI
`az login`
  
### Policy
  
1. Create policy that denies creation of resources that do not have tags.
2. Apply policy to subscription with the name 'tagging-policy'.
3. Use `az policy assignment list` to show result. 


### Packer
(*note: when installing packer on Windows, make sure you also manually include the environment variables in the path so that you can run packer from CLI.)
1. Create image reseource group using `az group create --location eastus --name packer-rg`.
2. Create Terraform Service Principle with `az ad sp create-for-rbac --role="Contributor" --name="TerraformSP"` and set the environment variables and Azure Subscription ID as follows:
···
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID="00000000-0000-0000-0000-000000000000"
export ARM_CLIENT_ID="00000000-0000-0000-0000-000000000000"
export ARM_CLIENT_SECRET="XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
export ARM_TENANT_ID="00000000-0000-0000-0000-000000000000"
echo "Done"
···
3. Create image with `packer build server.json`.
  
    
### Terraform
1. Plan Terraform with `terraform plan -var-file terraform.tfvars -out tfplan.out`.
2. Apply deployment with `terraform apply "tfplan.out"`.
3. Lastly, destroy Terraform resource with `terraform destroy` and delete image with `az image delete -g packer-rg -n my-packer-image`.

  


