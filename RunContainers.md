# Run Containers by Using Azure Container Instances

### 1. Housekeeping

- Open an incognito or in-private window, and log in to the Azure portal using the username and password provided in the lab environment.
- From within the portal, initiate the Cloud Shell, and when prompted, select a Bash shell (versus PowerShell).
- When prompted, choose "Mount a Storage Account."
- Choose the lab subscription and click Apply.
- Select the storage account that's already been deployed for you.
- Select the one, existing, resource group.
- Create a new fileshare and name it "fileshare" (all lower-case)
- Click Apply.
- Wait for the command prompt to appear.

### 2. Create an instance of Azure Container Registry

From the Bash command prompt in Cloud Shell:

- Retrieve the name of the resource group already deployed in the lab environment using the az group list command,

  ```bash
  az group list
  ```

- Set up three variables as follows:

  ```bash
  rg=<SOURCE_GROUP_NAME>
  name=acrlabdemo
  acr="$name$RANDOM"
  ```

- Set up a new ACR using the az acr create command.
  You will need to pass arguments for the resource group, the name of the new ACR, and the service tier, or SKU.
  Hint: Use the rg and acr environment variables for the first two arguments, and set the SKU to Basic.

  ```bash
  az acr create --resource-group $rg --name $acr --sku Basic

  ```

- Enable an admin user for the registry using the az acr update command.
  You will need to pass arguments for the ACR name (using the acr environment variable) and then set the admin-enabled argument to true.

  ```bash
  az acr update -n $acr --admin-enabled true

  ```

### 3. Build and Push a Container Image to ACR

- You should still be in the Cloud Shell session you had opened when creating the ACR instance.
- Change to the clouddrive directory with cd clouddrive.

  ```bash
  cd clouddrive

  ```

- Create a simple, one-line Dockerfile, called "Dockerfile" with the command, below, which will create the file in your clouddrive directory.

  ```bash
  echo FROM mcr.microsoft.com/hello-world > Dockerfile
  ```

- Build (and push) a new imagine in your ACR, using the Dockerfile you just created using the az acr build command.
  You will need to pass three arguments: the image, the registry name, and the Dockerfile name.

  Hints: The value for the --image argument is sample/hello-world:v1.
  After the argument for the Dockerfile name, add a space and then a period (".");
  the period indicates that the file can be found at the root of the current directory, which is clouddrive.
  If you leave out the period, you will likely get an error.
  The build and push will take a few minutes to complete.

  ```bash
  az acr build --image sample/hello-world:v1 --registry $acr --file Dockerfile .

  ```

- Close or minimize the Cloud Shell, and return to the resource group overview page in the portal.
- Find and select the new ACR instance and go to Repositories to confirm that the image exists in the repository.

### 4. Deploy an Image to Azure Container Instances (ACI)

In the Azure portal, create a new ACI. Ensure that you:

- Assign it to the existing resource group; do not create a new one.
- Leave the region defaulted, and name your container anything you wish.
- Use the image stored in your ACR.
  Hint: Once you select Azure Container Registry for the Image Source,
  it should default to your ACR and the sample image. If not, see the troubleshooting tips, below.

- Skip all other tabs in the wizard, and proceed to review and create the ACI. It will take a few minutes to deploy.
- Go to the resource and select Start. You can monitor the start-up progress in Notifications.
- When the container has started, navigate to Containers and click Logs to confirm that your installation is working.

  ```bash
  az container logs --resource-group $rg --name myacicontainer
  ```

`Troubleshooting:`

- When working through the ACI wizard, if the ACR and image do not appear automatically when you choose Azure Container Registry for the Image Source, you may need to refresh the admin access (which you did at the command line earlier in the lab). To do that in the portal, return to the ACR Overview page, and select Update near the top of the page. Toggle the Admin user to Disabled and Save. Then, toggle the Admin user back to Enabled and Save again. Return to the ACI wizard, and you should see the ACR and the sample image available in the registry and image fields.
- When you start your container in ACI, you may get an error message that says the container is "still transitioning." Wait a couple of minutes and try again.
