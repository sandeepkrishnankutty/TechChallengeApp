# Summary

For this exercise I am using Azure as the cloud service provider. Other solutions used are as below
    CI/CD - Azure Devops
    Infrastructure Automation: Azure ResourceManager Templates.
    SecretStorage - Azure Keyvault/Azure Devops
    Container Registry - Azure Container Registry
    Container Platform - Webapp for Containers
    PostgreSQL - Azure Postgresql

# Architecture of the solution

##### Prerequisites

1. Azure Container registry with admin enabled: This is to store the containers
2. Azure Keyvault to store secret variables.
3. Update the confg.toml file to replace the secret values with secrets from Azure Devops or Keyvault.
4. Update to db/db.go to fix bug.

##### Solution
###### Build
Azure devops YAML pipeline (./devops/deploy/azure-pipelines.yml)
1. Checkout the repo
2. Transform the config.toml to replace the secrets.
3. Build the docker image
4. Push to docker image to ACR
5. Export the ARM template as artifact.(./devops/provision/template.json)

###### Deploy
Azure devops YAML pipeline (./devops/deploy/azure-pipelines.yml)
1. Download the pipeline artifact
2. Deploy the ARM template from Artifact.
3. Deploy to Webapp for containers Staging pulling from ACR
4. Swap Staging with production
![Architecture](./azure.jpg?raw=true)
# Future Improvements of the solution
1. Implement Azure AppService Autoscale for scaling automatically.
2. Deploy to multiple regions for resiliency and use Azure Application Gateway/Front door for Security and loadbalancing.
3. Multi region of Postgresql for resiliency.
4. Update application to read from docker secrets rather than from config file.
