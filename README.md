# azure-devops

Q1 - SCENARIO
A car rental company called FastCarz has a .net Web Application and Web API which are recently migrated from on-premise system to Azure cloud using Azure Web App Service
and Web API Service.
The on-premises system had 3 environments Dev, QA and Prod.
The code repository was maintained in TFS and moved to Azure GIT now. The TFS has daily builds which triggers every night which build the solution and copy the build package to drop folder.
deployments were done to the respective environment manually. The customer is planning to setup Azure DevOps service for below requirements:

1) The build should trigger as soon as anyone in the dev team checks in code to master branch.
  **Trigger to the build pipeline is done using the trigger section in azure-pipelines.yml file **
  
2) There will be test projects which will create and maintained in the solution along the Web and API. The trigger should build all the 3 projects - Web, API and test.
   The build should not be successful if any test fails.
  **In the yml file, the step "Run Unit Test case and collect code coverage" will calcualte the code coverage and also fail the build if any of the test project's test cases fail**
  
3) The deployment of code and artifacts should be automated to Dev environment. 
  **Currently the deployment to Development environment is in the YML file itself. The developer can choose weather to deploy or not based on the Variable set at run time to the build**
  
4) Upon successful deployment to the Dev environment, deployment should be easily promoted to QA and Prod through automated process.
  **Further Environment deployment can be added to steps by adding "Deployment" stages**
  
5) The deployments to QA and Prod should be enabled with Approvals from approvers only.
  **Approvals can be set in environments section of Azure DevOps Stages**
  
------------------------------

Q2 - SCENARIO
Macro Life, a healthcare company has recently setup the entire Network and Infrastructure on Azure. 
The infrastructure has different components such as Virtual N/W, Subnets, NIC, IPs, NSG etc.
The IT team currently has developed PowerShell scripts to deploy each component where all the properties of each resource is set using PowerShell commands.
The business has realized that the PowerShell scripts are growing over period of time and difficult to handover when new admin onboards in the IT.
The IT team has now decided to move to ARM based deployment of all resources to Azure.
All the passwords are stored in a Azure Service known as key Vault. The deployments needs to be automated using Azure DevOps using IaC(Infrastructure as Code).

1) What are different artifacts you need to create - name of the artifacts and its purpose
  **The artifacts needed to create and deploy resources using ARM templates are template.json and prameters.josn. Using these two files and also Azure ARM deployment step, resources can be created or updated in Azure from Azure Devops, after creating a service principal**
  
2) List the tools you will to create and store the ARM templates.
  **ARM template can be stored and version controlled in any repo. preferabbly in Azure Devops Git repo also merges to be enforced using PR mechanism with automated review and testing**
  
3) Explain the process and steps to create automated deployment pipeline. 
  **Automated deployment can be created using a trigger on a Build pipleine. If any build is triggered then the continious deployment trigger can be set**
  
4) Create a sample ARM template you will use to deploy a Windows VM of any size
  **The sample ARM template is template.json, which can deploy a vM with basic configuration. THe Size can be set using the Parameter file and also read the VM Admin password from Azure Vault**
  
5) Explain how will you access the password stored in Key Vault and use it as Admin Password in the VM ARM template.
  **The access to valut in VM can be set by referencing the vault Resource ID and the service principal using it to deploy should have access to valut**

------------------------

Q3 - SCENARIO
A Toy Retail company ToyTrex has it retail application deployed as 3-tier application - Web App(UI), Web API(middle layer) and Database as Azure SQL.
The user load started increasing multiple fold every month and complex programs getting implemented, the application started performing poorly.
As a result, company decided to re-architect the middle layer as microservices using Azure Kubernetes Services.
The new architecture has below design decisions.

1) The middle layer should be implemented as Microservices using Azure AKS
  **The Implementation in azure-pipelines.yml have the implementation of creating the docker image, uploading it to ACR and also creating a deployment to ACI. AKS deployment, can be done using a HELM chart**
2) The middle layer API should be deployed as containerized application images
   **The Image upload step is coded in stage - "Upload to ACR"**
3) The container images will use Azure Container Repository (ACR) as the private image repository
  **ACR repo by default is private and access to it can be created by setting up a serivce connection, in the Project setting of Azure DevOps**
4) The CI/CD pipelines for microservices should be implemented using Azure DevOps services.
  **CI & CD can be implemented in Azure DevOps either using a yml pipelines or can be done in build and the images can be deployed by release pipleines.**
5) The Azure DevOps should be able to access ACR and download the container images for microservices deployment
  **By setting up the service connection, the Azure DevOps pipeline can upload and download the images**
6) The image should be deployed as templates such as <image_name>:<build_id>
  **The step "Upload to ACR" currently tags the images. the tags can also set in multi lines**

Hopefully, this helps to understand the code implemented in the Repo. 
