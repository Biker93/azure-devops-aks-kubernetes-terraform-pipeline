=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# Azure Devops

The current LIVE clusters are in the "Hosting-Production" subscription
   preprod    in RG hosting-preproduciton-aks
   production in RG hosting-prod-aks

make sure whatever subscription/RG is used for this testing does not overlap


created an Azure DevOps project
https://dev.azure.com/AmericanInstitutesForResearch/Terraform-AKS/_settings/
kthomson@air.org is Project administrator


but I don't know how to see this in portal.azure.com ... perhaps under kthomson rather than pcrp_kthomson?
https://portal.azure.com/#@air.org/dashboard/private/7280f459-e037-44c4-93a1-6111be878015 
https://aex.dev.azure.com/me?mkt=en-US
  this account shows the 3 Azure DevOps Organizations:
    dev.azure.com/American-Institutes-for-Research (Owner)
    kipthomson.visualstudio.com (Owner)
    dev.azure.com/AmericanInstitutesForResearch (Member)
on that last page/section: click on "Manage Security" ...
    can get "personal access token"
    SSH public keys (already set one)
    Authorizations

and there is a link to my Visual Studio Subscription
  https://my.visualstudio.com/Benefits?wt.mc_id=o~msft~profile~devprogram_attach&workflowid=devprogram&mkt=en-us

*** I may need to set the "default" subscription so "az" commands are targeted to the right environment ***


=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# Terraform prototype

Following this course section 33: Using Terraform & Azure DevOps Provision Azure AKS cluster
https://www.udemy.com/course/azure-kubernetes-service-with-azure-devops-and-terraform/learn/lecture/23644036#overview
https://github.com/stacksimplify/azure-aks-kubernetes-masterclass/tree/master/25-Azure-DevOps-Terraform-Azure-AKS
https://github.com/stacksimplify/azure-devops-aks-kubernetes-terraform-pipeline
https://github.com/stacksimplify/azure-devops-github-acr-aks-app1


Step 02  *** using SAFARI for MSDN accounts ***
https://biker93.visualstudio.com    (sign in)
install the module in Organization Biker93
https://marketplace.visualstudio.com/items?itemName=charleszipp.azure-pipelines-tasks-terraform

Step 03
Review

Step 04 (201)
I forked the repo so I don't have to create/push/etc
azure-devops-aks-kubernetes-terraform-pipeline

Step-05: Create New Azure DevOps Project for IAC
create Project
terraform-azure-aks
Provision Azure AKS Cluster using Azure DevOps & Terraform

Step-07: Create Azure RM Service Connection for Terraform Commands
Settings
Pipelines -> Service Connections -> Create Service Connection
terraform-aks-azurerm-svc-con
Azure RM Service Connection for provisioning AKS Cluster using Terraform on Azure DevOps
failed:
  Could not authenticate to Azure Active Directory. If a popup blocker is enabled in the browser, disable it and try again.
in Safari, Pref/Websites/Pop-up Windows ... ALLOW all
  refresh browser and try again: it did require I re-authenticate to Azure ... and now it works

Step-08: VERY IMPORTANT FIX: Provide Permission to create Azure AD Groups
open terraform-aks-azurerm-svc-con and "Manage Service Accout"
*** this works ... it failed on the AIR DevOps subscription ***

Starting June 30th, 2020 we will no longer add any new features to Azure AD Graph API. We strongly recommend that you use Microsoft Graph API instead of Azure AD Graph API to access Azure Active Directory resources.  Learn more
https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363

click the checkbox on left and "Add"
at bottom, should see green check by "Granted for Default Directory"

Step-09: Create SSH Public Key for Linux VMs

mkdir $HOME/ssh-keys-terraform-aks-devops
ssh-keygen \
    -m PEM \
    -t rsa \
    -b 4096 \
    -C "azureuser@myserver" \
    -f ~/ssh-keys-terraform-aks-devops/aks-terraform-devops-ssh-key-ububtu \
ls -lrt $HOME/ssh-keys-terraform-aks-devops
-rw-------  1 kthomson  staff  3243 Sep  9 23:36 aks-terraform-devops-ssh-key-ububtu
-rw-r--r--  1 kthomson  staff   744 Sep  9 23:36 aks-terraform-devops-ssh-key-ububtu.pub


Step-10: Upload file to Azure DevOps as Secure File



Step-11: Create Azure Pipeline to Provision AKS Cluster


Initializing the backend...

Successfully configured the backend "azurerm"! Terraform will automatically
use this backend unless the backend configuration changes.

│ Error: Failed to get existing workspaces: Error retrieving keys for Storage Account "terraformstatexlrwdrzs": storage.AccountsClient#ListKeys: Failure responding to request: StatusCode=404 -- Original Error: autorest/azure: Service returned an error. Status=404 Code="ResourceGroupNotFound" Message="Resource group 'terraform-storage-rg' could not be found."

##[error]Terraform command 'init' failed with exit code '1'.
##[error]╷
│ Error: Failed to get existing workspaces: Error retrieving keys for Storage Account "terraformstatexlrwdrzs": storage.AccountsClient#ListKeys: Failure responding to request: StatusCode=404 -- Original Error: autorest/azure: Service returned an error. Status=404 Code="ResourceGroupNotFound" Message="Resource group 'terraform-storage-rg' could not be found."

Finishing: Terraform Init

*** need to create a storage account and put the name in the tf file ***
demo in 185: step 16
https://www.udemy.com/course/azure-kubernetes-service-with-azure-devops-and-terraform/learn/lecture/23628396#overview










He is using Github ... I'm using Azure Repos ... have to see if there is any functional difference
"create local folder" 
try to clone from Azure Repo to local (using VScode)
> git clone https://AmericanInstitutesForResearch@dev.azure.com/AmericanInstitutesForResearch/Terraform-AKS/_git/Terraform-AKS /Users/kthomson/Terraform-AKS --progress
fatal: Authentication failed for 'https://dev.azure.com/AmericanInstitutesForResearch/Terraform-AKS/_git/Terraform-AKS/'

changed Azure Repo clone to SSH, added SSH key, but still could not "Clone in VSc" ... had to use terminal and git clone:
git clone git@ssh.dev.azure.com:v3/AmericanInstitutesForResearch/Terraform-AKS/Terraform-AKS

https://docs.microsoft.com/en-us/azure/devops/repos/git/use-ssh-keys-to-authenticate?view=azure-devops

so ... 
my current DevOps Repo file for the Terraform-AKS project corresponds to his "azure-devops-aks-kubernetes-terraform-pipeline"
  (the class had a PARENT folder with an earlier non-Terraform folder azure-devops-github-acr-aks-app1)
I have already created local, etc etc .. so skip rest of Step 04

Step 05: (202)
I already created the Project "Terraform-AKS" 
my Project corresponds to his Project = "terraform-azure-aks"

(no Step 06)

Step 07:
Service Connection Name: terraform-aks-azurerm-svc-con
Azure RM Service Connection for provisioning AKS Cluster using Terraform on Azure DevOps

open the Project Overview page ... Settings "Gear" is in the very bottom left 
Open Service Connections


│ Error: creating Managed Kubernetes Cluster "terraform-aks-dev-cluster" (Resource Group "terraform-aks-dev"): containerservice.ManagedClustersClient#CreateOrUpdate: Failure sending request: StatusCode=0 -- Original Error: Code="WindowsProfilePasswordInvalid" Message="Invalid adminPassword. Error: Length of password is invalid. Required length: [14, 123]. Minimum password length required by AKS for AzSecPack is longer. Please see https://docs.microsoft.com/en-us/rest/api/compute/virtualmachinescalesets/createorupdate#virtualmachinescalesetosprofile"


*** re-running job does not seem to pull updated repo code ***
started a NEW job ... that got the changed password length and completed!!

az aks get-credentials --resource-group terraform-aks-dev  --name terraform-aks-dev-cluster --admin
*** error *** because I never used this account in terminal!

az login   #in the Safari/MSDN browser
kubectl config get-contexts
cp ~/.kube/config ~/.kube/config-210911
az aks get-credentials --resource-group terraform-aks-dev  --name terraform-aks-dev-cluster --admin
kubectl config get-contexts

az aks nodepool list --cluster-name terraform-aks-dev-cluster --resource-group terraform-aks-dev -o table
