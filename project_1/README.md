# spfx

## Summary

Short summary on functionality and used technologies.

[picture of the solution in action, if possible]

## Used SharePoint Framework Version

![version](https://img.shields.io/badge/version-1.21.1-green.svg)

## Applies to

- [SharePoint Framework](https://aka.ms/spfx)
- [Microsoft 365 tenant](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-developer-tenant)

> Get your own free development tenant by subscribing to [Microsoft 365 developer program](http://aka.ms/o365devprogram)

## Prerequisites

> Any special pre-requisites?

## Solution

| Solution    | Author(s)                                               |
| ----------- | ------------------------------------------------------- |
| folder name | Author details (name, company, twitter alias with link) |

## Version history

| Version | Date             | Comments        |
| ------- | ---------------- | --------------- |
| 1.1     | March 10, 2021   | Update comment  |
| 1.0     | January 29, 2021 | Initial release |

## Disclaimer

**THIS CODE IS PROVIDED _AS IS_ WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT.**

---

## Minimal Path to Awesome

- Clone this repository
- Ensure that you are at the solution folder
- in the command-line run:
  - **npm install**
  - **gulp serve**

> Include any additional steps as needed.

## Features

Description of the extension that expands upon high-level summary above.

This extension illustrates the following concepts:

- topic 1
- topic 2
- topic 3

> Notice that better pictures and documentation will increase the sample usage and the value you are providing for others. Thanks for your submissions advance.

> Share your web part with others through Microsoft 365 Patterns and Practices program to get visibility and exposure. More details on the community, open-source projects and other activities from http://aka.ms/m365pnp.

## References

- [Getting started with SharePoint Framework](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-developer-tenant)
- [Building for Microsoft teams](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/build-for-teams-overview)
- [Use Microsoft Graph in your solution](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/get-started/using-microsoft-graph-apis)
- [Publish SharePoint Framework applications to the Marketplace](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/publish-to-marketplace-overview)
- [Microsoft 365 Patterns and Practices](https://aka.ms/m365pnp) - Guidance, tooling, samples and open-source controls for your Microsoft 365 development


## codes to setup 

 - create project folder
 - cd into the project folder and run the command - docker run -it --rm --name spfx-helloworld -v ${PWD}:/usr/app/spfx -p 4321:4321 -p 35729:35729 m365pnp/spfx
 - since you are in docker interactive mode using the -it, once container is started, you will be launched into the path of your image usr/app/spfx
 - run your yeoman generator from inside the container using yo @microsoft/sharepoint
 - provide details webpart if you are installing a webpart and other details.
 - add line to config/write-manifest.json - "debugBasePath": "https://localhost:35729" 
 - add line to config/serve.json - "hostname": "0.0.0.0",
 - update the initial page in config/serve.json also
 - run gulp trust-dev-cert in interactive mode
 - run gulp serve and paste the initial page url that you have earlier updated in the browser where you are signed into sharepoint and open the webpart.


## git setup

- install git in your machine and open vs code.
- initialise the repo
- stage the changes by right clicking the changes and clik stage the changes

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
