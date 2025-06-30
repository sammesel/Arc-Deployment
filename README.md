# Arc-Deployment
here you'll find step-by-step instructions to deploy Arc-enabled servers, including SQL Server

# Required Permissions (for the person doing the onboarding):

the original documentation is available at: https://learn.microsoft.com/en-us/azure/azure-arc/servers/prerequisites#required-permissions, for your convenience is duplicated below:

**You'll need the following Azure built-in roles for different aspects of managing connected machines:**

* To onboard machines, you must have the Azure Connected Machine Onboarding or Contributor role for the resource group where you're managing the servers.
* To read, modify, and delete a machine, you must have the Azure Connected Machine Resource Administrator role for the resource group.
* To select a resource group from the drop-down list when using the Generate script method, you'll also need the Reader role for that resource group (or another role that includes Reader access).
* When associating a Private Link Scope with an Arc Server, you must have Microsoft.HybridCompute/privateLinkScopes/read permission on the Private Link Scope Resource.

## Resource Providers
In order to the Arc-enabled resources to communicate with Azure, the following Azure Resource Providers are required:<br><br>
* Microsoft.HybridCompute<br>
* Microsoft.GuestConfiguration<br>
* Microsoft.HybridConnectivity<br>
* Microsoft.AzureArcData (if you plan to Arc-enable SQL Servers)<br>
* Microsoft.Compute (for Azure Update Manager and automatic extension upgrades)<br>
<br>
To register these Resource Providers, you can either use the Portal, Azure PowerShell, or Azure CLI. 
The URL https://learn.microsoft.com/en-us/azure/azure-arc/servers/prerequisites#azure-resource-providers contains instructions on how to register these Resource providers 

## Agent requirements

## Log Analytics

## Obtaining the Scripts to Onboard Client Agent
