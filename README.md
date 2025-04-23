# Developing Solutions for Microsoft Azure

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
