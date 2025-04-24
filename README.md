# Developing Solutions for Microsoft Azure

### Resources

- [Develop Azure Functions by using Visual Studio Code](https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-vs-code?tabs=csharp)
- [Set up staging environments in Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/deploy-staging-slots?tabs=portal)
- [Language runtime support policy for Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/language-support-policy?tabs=windows)
- [Set scaling rules in Azure Container Apps](https://learn.microsoft.com/en-us/azure/container-apps/scale-app?pivots=azure-cli)
- [What is Service Connector?](https://learn.microsoft.com/en-us/azure/service-connector/overview)
- [Deploy an app into a container in Azure or Docker Hub](https://learn.microsoft.com/en-us/visualstudio/containers/deploy-containerized?view=vs-2022)
- [What is Azure Container Instances?](https://learn.microsoft.com/en-us/azure/container-instances/container-instances-overview)
- [YAML reference: Azure Container Instances](https://learn.microsoft.com/en-us/azure/container-instances/container-instances-reference-yaml)
- [Azure Samples - GitHub](https://github.com/Azure-Samples)
- [Azure App Service pricing](https://azure.microsoft.com/en-us/pricing/details/app-service/windows/)
- [Azure Container Registry tasks](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-tasks-overview)
- [Shared responsibility in the cloud](https://learn.microsoft.com/en-us/azure/security/fundamentals/shared-responsibility)

---

### Migrate a Website to Azure Web Apps

- Install IIS on the Virtual Machine and Create a Simple Website
- Download and Install the [App Service Migration Assistant](https://learn.microsoft.com/en-gb/azure/app-service/app-service-asp-net-migration#app-service-migration-tools-and-resources)
- Configure the App Service Migration Assistant to Migrate the Website
- Confirm the Website Has Been Successfully Migrated

---

```bash
# Install IIS #
Install-WindowsFeature -Name Web-Server -IncludeAllSubFeature -IncludeManagementTools

# Create simple HTML website #
echo '<!doctype html><html><body><h1>Hello Cloud Gurus!</h1></body></html>' > C:\inetpub\wwwroot\index.html
```
