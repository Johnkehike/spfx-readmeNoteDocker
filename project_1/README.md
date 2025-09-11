How to setup devops pipeline for SPFx projects

History of pem certificate generation commands
 1144  pwd
 1145  mkdir blog
 1146  mkdir blog-spfx
 1147  cd blog-spfx
 1148  ls
 1149  docker run -it --rm --name ${PWD##*/} -v $PWD:/usr/app/spfx -p 4321:4321 -p 35729:35729 m365pnp/spfx
 1150  cd Node/js
 1151  ls
 1152  lopenssl genrsa -out mykey.key 2048\n
 1153  lopenssl genrsa -out mykey.key 2048
 1154  openssl genrsa -out mykey.key 2048
 1155  openssl req -new -key mykey.key -out mycsr.csr
 1156  openssl x509 -req -days 365 -in mycsr.csr -signkey mykey.key -out mycert.crt
 1157  openssl pkcs12 -export -out mycert.pfx -inkey mykey.key -in mycert.crt
 1158  # openssl pkcs12 -in mycert.pfx -out mycert.pem -nodes
 1159  openssl pkcs12 -in mycert.pfx -out mycert.pem -nodes

 references
 https://chuvash.eu/2020/deploying-spfx-using-office-365-cli-custom-aad-app-and-azure-pipelines/
 https://www.xolphin.com/support/Certificate_conversions/Convert_pfx_file_to_pem_file
 https://pnp.github.io/cli-microsoft365/cmd/login/
 https://learn.microsoft.com/en-us/azure/devops/pipelines/library/secure-files?view=azure-devops
 

Setup SPFx in Docker

Have you ever being tired of jumping between different node versions in yoour SharePoint framework development career? NVM came for the rescue as developers were able to switch between different node versions on the same machine. however that wasn't not so helpful as SPFx required different versions of other libraries based on the node version being used. so your yoeman generator version had to be the right one for your project. and other libraris like gulp also was also required. if you are like me, that requires other global version of these libraries for other projects, it eventually becomes hectic managing different versions of software for different projects leading to unavoidable errors in most cases. 

I will be demostrating how to use docker containers to manage SPFx projects even without local installation of node on your machine allowing you to spin up projects faster and test your configurations locally. in our next article, we will also be looking at deploying your project in what i call the enterprise way leveraging azure devops to deploy SPFx packages to app catalog sites.

requirements
sign up to dockerhup and take a look at the microsoft official docker image for SPFx/pnpj in dockerhub.com
i'm sure git should be handy but if you are new to git, download and install git - (not a major requirement).
create a folder you are using for your project in your local machine - this is where you will store the codes from your container and work with your codes locally in VSCode
download and install docker desktop and run the app using your signed up account from earlier, login to the app
enable file sharing for the folder created in docker desktop by going to settings then resources and go to the file sharing tab and browse the folder for your project locally then click the add button to share the folder of your chosen

Installation
open command prompt either via terminal prompt in vscode or using your command prompt whichever works best for you. cd into your project folder and run the command below
docker run -it --rm --name spfx-helloworld -v ${PWD}:/usr/app/spfx -p 4321:4321 -p 35729:35729 m365pnp/spfx
m365pnp/spfx is the base image in dockerhub which your container will be created from.
-v flag maps your current folder directory to the usr/app/spfx directory in yourcontainer.
-it gives you an interactive session to the docker container where you can continue with your installation. so you will noticed you are on the prompt usr/app/spfx in your command prompt after the command finish running.

next you want to run the yeoman generator inside the container using yo @microsoft/harepoint  - from here proceed with your spfx project installation steps as normal.

after answering all the questions in the project setup wizard/steps, you can then do the usual gulp trust-dev-cert to install the certificate needed .....
finally make the below change to the your project and then run gulp trust-dev-cert && gulp serve to see your work locally
 - add a line to the config/serve.json file - "ipAddress": "0.0.0.0",
once gulp serve is running, take the workbecnh url for your SPO site and test in your browser to see your project. - eg https://xxxxx.sharepoint.com/_layouts/15/workbench.aspx
as the code is running from your docker container, first run the url http://localhost:35729 before loading your workbench.
open the url in unsafe mode before open

if you have an old project, there are SPFx images for older versions of SPFx. you can find the list here. - https://hub.docker.com/r/m365pnp/spfx.
N/B to run the image on an existing project, run the command followed by gulp trust-dev-cert and gulp serve

references
- Danny Jessee (2023). _Scaling up a SharePoint Framework Development Team_ [Scaling up SharePoint Framework Development for Enterprises]. https://app.pluralsight.com/library/courses/scaling-up-sharepoint-framework-development-enterprises/table-of-contents [2/9/2025]
- Microsoft 365 Patterns and Practices (2025) m365pnp/spfx []. https://hub.docker.com/r/m365pnp/spfx [2025]
- https://learn.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-development-environment
- https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/get-started/build-a-hello-world-web-part





modified
How to Set Up SPFx in Docker

If you’ve ever been frustrated by constantly switching between different Node.js versions during your SharePoint Framework (SPFx) development, you’re not alone. Tools like NVM make it easier by letting developers switch Node versions on the same machine. However, SPFx projects often require specific versions of other libraries, like the Yeoman generator and Gulp, which can be a headache to manage. If you work on multiple projects that require different global versions of these tools, managing software versions quickly becomes complex—often leading to unavoidable errors.

In this article, I’ll demonstrate how to use Docker containers to manage SPFx projects—without needing specific Node.js versions installed locally. This approach allows you to spin up different projects faster and test configurations locally. In a follow-up article, I’ll cover how to deploy SPFx packages to app catalog sites using Azure DevOps for a more enterprise-ready workflow.

Requirements:

1. Sign up for Docker Hub and review the official Microsoft Docker image for SPFx/pnpjs on dockerhub.com.

2. (Optional) Install Git if you don’t have it already. It’s helpful, but not absolutely required.

3. Create a folder on your local machine for your project. You’ll use this to store code from your container and work locally in VS Code.

4. Download and install Docker Desktop, then log in with your Docker Hub account.

5. Enable file sharing for your project folder in Docker Desktop: go to Settings > Resources > File Sharing, then browse for your folder and add it.

Installation:



1. Open your command prompt or VS Code terminal.

2. Navigate (cd) to your project folder.

3. Run the following command:



   docker run -it --rm --name spfx-helloworld -v ${PWD}:/usr/app/spfx -p 4321:4321 -p 35729:35729 m365pnp/spfx



   - m365pnp/spfx is the base image from Docker Hub.

   - The -v flag maps your local folder to /usr/app/spfx in the container.

   - The -it flag gives you an interactive session in the Docker container.



After the command finishes, you’ll be at the /usr/app/spfx prompt inside your container.

Next, run the Yeoman generator inside the container using:



   yo @microsoft/sharepoint



Proceed with the normal SPFx project setup steps.

After completing the project setup wizard, run:



   gulp trust-dev-cert





to install the necessary certificate. Then, make the following change to your project before running gulp trust-dev-cert && gulp serve to see your work locally.

Add the following line to your config/serve.json file:

*    "ipAddress": "0.0.0.0",

Once gulp serve is running, take the workbench URL for your SharePoint Online site and test your project in the browser (e.g., https://xxxxx.sharepoint.com/_layouts/15/workbench.aspx). If required open the URL http://localhost:4321 before opening your workbench.

If you have an existing project with an older SPFx version, there are Docker images available for older versions. Find the list here: https://hub.docker.com/r/m365pnp/spfx. To run the image on an existing project, use the appropriate command, then run gulp trust-dev-cert and gulp serve as usual.

references

* Danny Jessee (2023). Scaling up a SharePoint Framework Development Team [Scaling up SharePoint Framework Development for Enterprises]. https://app.pluralsight.com/library/courses/scaling-up-sharepoint-framework-development-enterprises/table-of-contents [2/9/2025]
* Microsoft 365 Patterns and Practices (2025) m365pnp/spfx []. https://hub.docker.com/r/m365pnp/spfx [2025]
* https://learn.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-development-environment
* https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/get-started/build-a-hello-world-web-part



## CREATE AZURE CONTAINER REGISTRY AND PUSH YOUR IMAGE FROM YOUR LOCAL DOCKER DESKTOP TO IT
#first created the jokeh ACR instance in a resource group of my choice and then used the command below to connect to Azure using Azure cli in vs code and completing the tagging of my image and uploading accordingly


az login --tenant acb5c3c9-6666-4768-bd0a-a8005dd65036
az acr login --name jokeh
## rename/retag the current local image of jokehi/jokeh to a tag in ACR - jokeh.azurecr.io
docker tag jokehi/jokeh jokeh.azurecr.io/jokeh
docker push jokeh.azurecr.io/jokeh


## Run SPFx docker from ACR
docker run -it --rm --name helloworld10 -v ${PWD}:/usr/app/spfx -p 4321:4321 -p 35729:35729 jokeh.azurecr.io/jokeh


after all stuffs
gulp trust-dev-cert
gulp serve
