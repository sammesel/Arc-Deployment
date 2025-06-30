# Arc-Deployment
here you'll find step-by-step instructions to deploy Arc-enabled servers, including SQL Server

# Required Permissions (for the person doing the onboarding):

the original documentation is available at: https://learn.microsoft.com/en-us/azure/azure-arc/servers/prerequisites#required-permissions, for your convenience is duplicated below:

**You'll need the following Azure built-in roles for different aspects of managing connected machines:**

* To onboard machines, you must have the **Azure Connected Machine** Onboarding or **Contributor** role for the resource group where you're managing the servers.
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
* Microsoft.Dashboard **is also recommended**
<br>
To register these Resource Providers, you can either use the Portal, Azure PowerShell, or Azure CLI. 
The URL https://learn.microsoft.com/en-us/azure/azure-arc/servers/prerequisites#azure-resource-providers contains instructions on how to register these Resource providers 

## Connected Machine agent network requirements

In order for the Arc-enabled Servers to connect to Azure, they use outbound communication via port 443. You need to open (firewall) communication to URLS listed at https://learn.microsoft.com/en-us/azure/azure-arc/servers/network-requirements?tabs=azure-cloud#urls <br>
<br>
To test connectivity from one server, open a PowerShell prompt and test the following script:<br>
> [!NOTE]
> replace the location below (eastus) with your deployment location your <br>
```
$location = "eastus" 
Test-NetConnection -Port 443 
Test-NetConnection -ComputerName aka.ms -Port 443 
Test-NetConnection -ComputerName download.microsoft.com -Port 443 
Test-NetConnection -ComputerName packages.microsoft.com -Port 443 
Test-NetConnection -ComputerName login.windows.net -Port 443 
Test-NetConnection -ComputerName login.microsoftonline.com -Port 443 
Test-NetConnection -ComputerName pas.windows.net -Port 443 
Test-NetConnection -ComputerName management.azure.com -Port 443 
Test-NetConnection -ComputerName his.arc.azure.com -Port 443 
Test-NetConnection -ComputerName guestconfiguration.azure.com -Port 443 
Test-NetConnection -ComputerName guestnotificationservice.azure.com -Port 443 
Test-NetConnection -ComputerName servicebus.windows.net -Port 443 
Test-NetConnection -ComputerName waconazure.com -Port 443 
Test-NetConnection -ComputerName blob.core.windows.net -Port 443 
Test-NetConnection -ComputerName dc.services.visualstudio.com -Port 443 
Test-NetConnection -ComputerName "san-af-$($location)-prod.azurewebsites.net" -Port 443 
```



## Agent requirements

To get a list of Operating Systems that support Arc-enabled Servers go to: https://learn.microsoft.com/en-us/azure/azure-arc/servers/prerequisites#supported-operating-systems <br>
To understand Software and System requirements go to: https://learn.microsoft.com/en-us/azure/azure-arc/servers/prerequisites#software-and-system-requirements <br>
To review the Local user logon Right for the Windows System go to: https://learn.microsoft.com/en-us/azure/azure-arc/servers/prerequisites#local-user-logon-right-for-windows-systems<br>


## Create a Resource Group

## Create a Service Principal (**SPN**)

A Service Principal can be used to onboard servers at scale, not necessary during your Proof-of-Concept (POC) phase. <br>
tbe 

* To create a service principal in Azure refer to the official Microsoft documentation at: https://learn.microsoft.com/en-us/entra/identity-platform/howto-create-service-principal-portal. <br>

 
* with POWERSHELL <br>
```
az ad sp create-for-rbac -n "<replace with your SPN>" --role owner --scopes  /subscriptions/<replace with your subscription-id>
```

> [!NOTE]
> when the SPN is created, Azure will generate an output providing you with the AppId, Password, and the TenantID.
> you need to copy these pieces of information, something in the lines of: <br><br>
> {<br>
>   "appId": "04da1cff-eeee-444f-aaaa-da9999999999",<br>
>   "password": "Xxx0X@xxxxXXxxXxX.XX9.999x9XXxxXxx9XxxxX",<br>
>   "tenant": "999x99999-xxxx-9x99-9xx9-999x99x9x999"<br>
> }<br>
>
<br>


## Log Analytics

## Obtaining the Scripts to Onboard Client Agent


