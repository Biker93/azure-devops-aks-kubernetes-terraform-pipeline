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

Other links
https://github.com/hashicorp/terraform-provider-azurerm/blob/main/examples/kubernetes/spot-node-pool/main.tf


Final Link Set - Safari

Portal:
https://portal.azure.com/#@kthomsonair.onmicrosoft.com/resource/subscriptions/cf71d4cd-095a-47ec-bca0-060c571abedf/resourceGroups/terraform-aks-test/overview

DevOps:
https://biker93.visualstudio.com/terraform-azure-aks/_build/results?buildId=39&view=logs&j=ebb496a5-b0ba-51c9-e535-6a91110d593c&t=ebb496a5-b0ba-51c9-e535-6a91110d593c

Costs:
https://portal.azure.com/#blade/Microsoft_Azure_CostManagement/CostAnalysis/scope/%2Fsubscriptions%2Fcf71d4cd-095a-47ec-bca0-060c571abedf


Final Link Set - CHROME

https://www.udemy.com/course/azure-kubernetes-service-with-azure-devops-and-terraform/learn/lecture/23644074#questions/15815870

https://github.com/stacksimplify/azure-aks-kubernetes-masterclass/tree/master/25-Azure-DevOps-Terraform-Azure-AKS

https://www.udemy.com/home/my-courses/learning/?p=9

https://marketplace.visualstudio.com/items?itemName=ms-devlabs.custom-terraform-tasks

https://marketplace.visualstudio.com/items?itemName=charleszipp.azure-pipelines-tasks-terraform

https://github.com/charleszipp/azure-pipelines-tasks-terraform/issues/163

https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster_node_pool

https://registry.terraform.io/providers/hashicorp/azuread/latest/docs

https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/resources/group

https://registry.terraform.io/providers/hashicorp/azuread/latest

https://github.com/hashicorp/terraform-provider-azuread

https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs

https://registry.terraform.io/providers/hashicorp/azurerm/latest

https://github.com/hashicorp/terraform-provider-azurerm/blob/main/examples/kubernetes/spot-node-pool/main.tf

https://github.com/Biker93/azure-devops-aks-kubernetes-terraform-pipeline

https://www.terraform.io/docs/extend/best-practices/naming.html

https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_machine

https://registry.terraform.io/providers/hashicorp/azurerm/2.17.0/docs/resources/kubernetes_cluster_node_pool

https://stacksimplify.com/azure-aks/create-windows-linux-virtualnodepools-using-az-aks-cli/

https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster_node_pool#example-usage

https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs

https://github.com/hashicorp/terraform-provider-azurerm/tree/main/examples/kubernetes

https://github.com/hashicorp/terraform-provider-azurerm/tree/main/examples/kubernetes/aci_connector_linux

https://learn.hashicorp.com/tutorials/terraform/troubleshooting-workflow?utm_source=WEBSITE&utm_medium=WEB_IO&utm_offer=ARTICLE_PAGE&utm_content=DOCS

https://www.terraform.io/upgrade-guides/0-15.html

https://learn.hashicorp.com/tutorials/terraform/versions

https://docs.microsoft.com/en-us/azure/aks/private-clusters

https://datatracker.ietf.org/doc/html/rfc1918

https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#limitations





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


=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# so problem with cloning ..

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


=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# WIndows Password length

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



=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# Windows OSSKU 

Error: creating/updating Managed Kubernetes Cluster Node Pool "win101" (Resource Group "terraform-aks-dev"): containerservice.AgentPoolsClient#CreateOrUpdate: Failure sending request: StatusCode=0 -- Original Error: Code="InvalidOSSKU" Message="OSSKU='Ubuntu' is invalid, details: Windows does not allow OSSKU selection"
│ 
on 10-aks-cluster-windows-user-nodepools.tf line 3, in resource "azurerm_kubernetes_cluster_node_pool" "win101":
│    3: resource "azurerm_kubernetes_cluster_node_pool" "win101" {


Added it manually to confirm parameters
only difference: the default (required?) disk size = 128GB so specifying 30GB may be the error

b/c I created it OUTSIDE of TF, get error whenrunning TF:
Error: A resource with the ID "/subscriptions/cf71d4cd-095a-47ec-bca0-060c571abedf/resourcegroups/terraform-aks-dev/providers/Microsoft.ContainerService/managedClusters/terraform-aks-dev-cluster/agentPools/win101" already exists - to be managed via Terraform this resource needs to be imported into the State. Please see the resource documentation for "azurerm_kubernetes_cluster_node_pool" for more information.
│ 

manually delete win101 and re-run
back to original error

https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster_node_pool


disable current pipeline


=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# rename all .tf to TEST/PROD

push
create new pipeline to test run from scratch --- JUST WINDOWS node pool
still getting error

Review the documentation ... again:
https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster_node_pool
of interest:

fips_enabled

os_sku - (Optional) OsSKU to be used to specify Linux OSType. Not applicable to Windows OSType. Possible values include: Ubuntu, CBLMariner. Defaults to Ubuntu. Changing this forces a new resource to be created.

os_type - (Optional) The Operating System which should be used for this Node Pool. Changing this forces a new resource to be created. Possible values are Linux and Windows. Defaults to Linux.

node_count - (Optional) The initial number of nodes which should exist within this Node Pool. Valid values are between 0 and 1000 and must be a value in the range min_count - max_count.

If enable_auto_scaling is set to false, then the following fields can also be configured:
node_count - (Required) The number of nodes which should exist within this Node Pool. Valid values are between 0 and 1000.



https://github.com/hashicorp/terraform-provider-azurerm/tree/main/examples/kubernetes

https://stacksimplify.com/azure-aks/create-aks-nodepools-using-terraform/

https://stacksimplify.com/azure-aks/create-windows-linux-virtualnodepools-using-az-aks-cli/



=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# create a Windows node from commandline, not Terraform

AKS_RESOURCE_GROUP=terraform-aks-test
AKS_CLUSTER=terraform-aks-test-cluster
# Create New Windows Node Pool 
az aks nodepool add --resource-group ${AKS_RESOURCE_GROUP} \
                    --cluster-name ${AKS_CLUSTER} \
                    --os-type Windows \
                    --name win101 \
                    --node-count 1 \
                    --enable-cluster-autoscaler \
                    --max-count 5 \
                    --min-count 1 \
                    --mode User \
                    --node-vm-size Standard_DS2_v2 \
                    --labels environment=production nodepoolos=windows app=dotnet-apps nodepool-type=user \
                    --tags environment=production nodepoolos=windows app=dotnet-apps nodepool-type=user \
                    --zones {1,2,3}

{
  "availabilityZones": [
    "1",
    "2",
    "3"
  ],
  "count": 1,
  "enableAutoScaling": true,
  "enableEncryptionAtHost": false,
  "enableFips": false,
  "enableNodePublicIp": false,
  "enableUltraSsd": false,
  "gpuInstanceProfile": null,
  "id": "/subscriptions/cf71d4cd-095a-47ec-bca0-060c571abedf/resourcegroups/terraform-aks-test/providers/Microsoft.ContainerService/managedClusters/terraform-aks-test-cluster/agentPools/win101",
  "kubeletConfig": null,
  "kubeletDiskType": "OS",
  "linuxOsConfig": null,
  "maxCount": 5,
  "maxPods": 30,
  "minCount": 1,
  "mode": "User",
  "name": "win101",
  "nodeImageVersion": "AKSWindows-2019-17763.2114.210811",
  "nodeLabels": {
    "app": "dotnet-apps",
    "environment": "production",
    "nodepool-type": "user",
    "nodepoolos": "windows"
  },
  "nodePublicIpPrefixId": null,
  "nodeTaints": null,
  "orchestratorVersion": "1.21.2",
  "osDiskSizeGb": 128,
  "osDiskType": "Managed",
  "osSku": null,
  "osType": "Windows",
  "podSubnetId": null,
  "powerState": {
    "code": "Running"
  },
  "provisioningState": "Succeeded",
  "proximityPlacementGroupId": null,
  "resourceGroup": "terraform-aks-test",
  "scaleSetEvictionPolicy": null,
  "scaleSetPriority": null,
  "spotMaxPrice": null,
  "tags": {
    "app": "dotnet-apps",
    "environment": "production",
    "nodepool-type": "user",
    "nodepoolos": "windows"
  },
  "type": "Microsoft.ContainerService/managedClusters/agentPools",
  "typePropertiesType": "VirtualMachineScaleSets",
  "upgradeSettings": {
    "maxSurge": null
  },
  "vmSize": "Standard_DS2_v2",
  "vnetSubnetId": null
}


check the version info

Initializing provider plugins...
- Finding hashicorp/azuread versions matching "~> 1.0"...
- Finding hashicorp/random versions matching "~> 3.0"...
- Finding hashicorp/azurerm versions matching "~> 2.0"...
- Installing hashicorp/azuread v1.6.0...
- Installed hashicorp/azuread v1.6.0 (signed by HashiCorp)
- Installing hashicorp/random v3.1.0...
- Installed hashicorp/random v3.1.0 (signed by HashiCorp)
- Installing hashicorp/azurerm v2.76.0...
- Installed hashicorp/azurerm v2.76.0 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.


=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# tried to switch to alternate MS extension ... but the tf code is not compatible ... and seems like an extreme solution
biker93 ... Org settings ... extensions ... delete old, run install from website 
*** must be in Safari to get correct account/org ***


=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# Back to a full build with only Linux 101 active

# Verify
az aks get-credentials --resource-group terraform-aks-test  --name terraform-aks-test-cluster --admin

# connection
az aks nodepool list --cluster-name terraform-aks-test-cluster --resource-group terraform-aks-test -o table

# launch sample apps
kubectl apply -R -f kube-manifests
kubectl get all -A
kubectl get svc
http://52.141.209.251/

Mgmt console:
http://52.154.154.193/  need credentials

https://github.com/stacksimplify/azure-aks-kubernetes-masterclass/tree/master/06-Azure-MySQL-for-AKS-Storage#readme
Step-07: Access Application

Username: admin101
Password: password101

Bingo!!

=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# Windows OS_SKU

tried to explicitly set SKU to null

   with azurerm_kubernetes_cluster_node_pool.win101,
│   on 10-aks-cluster-windows-user-nodepools.tf line 14, in resource "azurerm_kubernetes_cluster_node_pool" "win101":
│   14:   os_sku                = ""

https://www.terraform.io/docs/extend/best-practices/naming.html


Kalyan confirmed he has the same result, so it is a bug in either Terraform or the Zipp plugin
I'm using current versions of both
Zipp Version	0.6.27	Released on	11/14/2018, 10:01:55 AM	Last updated	7/22/2021, 10:40:14 AM
this bug is not listed on
https://marketplace.visualstudio.com/items?itemName=charleszipp.azure-pipelines-tasks-terraform

the class was recorded > 11/4/20 using version 0.5.16 11/14/18 release 11/4/20 update
However, I don't see how to install a different version. The install page doesn't give an option
Imight be able to download an earlier version, but how to install in the DevOps Organization extensions


I could also change the TERRAFORM version to something about that date.
Current: /usr/local/bin/terraform version  Terraform v1.0.6  on linux_amd64
https://learn.hashicorp.com/tutorials/terraform/versions
  try 0.15.0
https://github.com/hashicorp/terraform/releases
https://www.hashicorp.com/blog/announcing-hashicorp-terraform-1-0-general-availability

no-go:
│ Error: Unsupported Terraform Core version
│ 
│   on 01-main.tf line 13, in terraform:
│   13:   required_version = "~> 0.15.0"
│ 
│ This configuration does not support Terraform version 1.0.6. To proceed,
│ either choose another supported Terraform version or update this version
│ constraint. Version constraints are normally set for good reason, so
│ updating the constraint may lead to other errors or unexpected behavior.


I submtted report to 
https://github.com/charleszipp/azure-pipelines-tasks-terraform/issues/163

Also found reported on 
https://githubmemory.com/repo/terraform-providers/terraform-provider-azurerm/issues?cursor=Y3Vyc29yOnYyOpK5MjAyMS0wOS0xM1QxMDo0MDoyMCswNTozMM47RkZ7&pagination=next&page=4


*** Kalyan reports he got it to work by upgrading JUST the azurerm version however I got an error  ***

=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# cont'

Messed around with different versions of Terraform, azurerm, groups, etc ...
Finally reset back to original EXCEPT for azurerm at 2.40.0

That works ... but only after completely deleting the cluster and the tfstate files

Another thing: when I tried upgrading to more current versions (>= rather than ~=) I got errors related to new options, esp in azuread:  
   name -> display_name
   add security_enabled=true
but this caused other problems so went back to ONLY azurerm upgrade

   3:   name        = "${azurerm_resource_group.aks_rg.name}-administrators"
│ This property has been renamed to `display_name` and will be removed in
│ version 2.0 of the AzureAD provider

etc.


https://registry.terraform.io/providers/hashicorp/azuread/latest/docs
https://registry.terraform.io/providers/hashicorp/azuread/latest
https://github.com/hashicorp/terraform-provider-azuread


https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/resources/group

=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# WORKING

Finally ...

re-enabled 10-win101 ... still working

run apps

# Verify
az aks get-credentials --resource-group terraform-aks-test  --name terraform-aks-test-cluster --admin

# connection
az aks nodepool list --cluster-name terraform-aks-test-cluster --resource-group terraform-aks-test -o table

# launch sample apps
kubectl apply -R -f kube-manifests
kubectl get all -A
kubectl get svc

https://github.com/stacksimplify/azure-aks-kubernetes-masterclass/tree/master/06-Azure-MySQL-for-AKS-Storage#readme
Step-07: Access Application

Mgmt console:
http://52.154.154.193/
Username: admin101
Password: password101

nginx:
http://52.141.209.251/

aspnet:
http://20.98.188.200


=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# 
=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
# 