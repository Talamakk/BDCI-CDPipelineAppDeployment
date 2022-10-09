# App deployment using CI/CD pipeline
This project shows how to build a Node.js Express app and deploy it to Azure Web App using CI/CD pipeline created in Azure DevOps. It was made mostly for DevOps training purposes, so any feedback is more than welcome!
## Implementation step by step
1. Prepare the app you want to deploy. For this project a Node.js Express Flatris app has been used. You can see original README.md clicking [here](https://github.com/skidding/flatris), a little sneak peek below:

[![Flatris](https://github.com/Talamakk/BDCI-CDPipelineAppDeployment/blob/main/Flatris-LAB/flatris.gif)](https://flatris.space/)

2. Prepare an Azure environment. There are a few ways to do it, from button clicking on the Azure portal, to creating PowerShell script (`New-AzAppServicePlan`, `New-AzWebApp` cmdlets). One another (and probably the most efficient) idea is to use IaC concept - *ARM template*. [Azure Resource Manager template](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/overview) enables to create infrastructure in a declarative way using JSON syntax. Instead of being built by sequence of programming commands, resources and their properties that need to be deployed are just definied in JSON file. This JSON file could be versioned and stored in project repository. IaC makes it very easy to manage infrastructure so it is the crucial part of DevOps concepts. That's why the ARM template was used in this project. The ARM template that you can find in these repo ([here](https://github.com/Talamakk/BDCI-CDPipelineAppDeployment/blob/main/ARM.json)) defines necessary serverless environment to run web app: [Azure App Service Plan](https://learn.microsoft.com/en-us/azure/app-service/overview-hosting-plans) (operating system, number of VMs, pricing tier) and [Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/overview-hosting-plans) (runtime, site config). The next step is to deploy definied infrastructure in previously created resource group:
```
New-AzResourceGroupDeployment `
-Name 'Deployment1' `
-ResourceGroupName 'DeploymentTest' `
-TemplateUri 'https://raw.githubusercontent.com/Talamakk/BDCI-CDPipelineAppDeployment/main/ARM.json' `
-webAppName 'BDFlatrisApp' `
-location 'West Europe' `
-sku 'B1'
```

3. Enable connection between prepared Azure environment and Azure DevOps service. Open the Azure DevOps project settings (*Project settings -> Service connections -> New service connection -> Azure Resource Manager -> Service Principal -> New Azure service connection*), than add created resource group:

<img src="https://github.com/Talamakk/BDCI-CDPipelineAppDeployment/blob/main/Images/1.JPG">



Next steps soon.  





