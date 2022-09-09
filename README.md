# azure_pipeline

**Migrate Java webapp from Github to Azure cloud using Azure pipeline (YAML)**

1] Create Azure account/subscription https://portal.azure.com

2] Create GitHub account {https://github.com/} and upload java webapp code

3] Directory structure for code (maven project):

   GitHub repo---mywebapp(anyfolder name)----src/main/webapp----index.jsp
   
   GitHub repo---mywebapp(anyfolder name)----src/main/webapp----WEB-INF-----web.xml
   
   GitHub repo---mywebapp(anyfolder name)----pom.xml
   
4] Create organisation and project in Azure devops {https://dev.azure.com/}
   Make sure to choose Git as version control while creating project. 
  ** 5 key components of Azure devops:**
  * Boards--------for planning
  * Repos---------for source codes
  * Pipelines-----for build and release automation
  * TestPlans-----provides tools to test your app 
  * Artifacts-----allows teams to share packages such as Maven, npm, NuGet....
   
5] Create Service connection between GitHub and Azure devops(ADO)
   ADO---Project---Project Settings----service connections----new Service connection----choose connection type as GitHub---Next---Authorize pipeline
   
6] Create appservice in Azure cloud. Appservice is platform as service (PAAS) to migrate any web app. 
   Azure cloud---app services--- +create---
   Subscription: choose one
   Resource group: create or choose
   web app Name: must be unique. This is URL of web app. 
   Publish: Code
   Run time stack: Java 11
   Java web server stack: apache tomcat 9.0
   os: linux
   Region: central US
   App service plan: 
            Sku and size: B1 (dev)
   Review +create
   Create
   
7] Create pipeline in ADO.
   ADO---pipelines---new pipeline (classic editor and YAML)
   Select GitHub Yaml
   Select a repo from GitHub
   Select Maven package java project web app to linux on azure
   select an Azure subscription
   continue
   sign in 
   select app service (web app) created earlier.
   validate and configure
   YAML file: azure-pipeline.yml is created with code. 
   Customize the YAML code: edit path of pom.xml per your requirement
    for this example mavenPomFile: '**mywebapp**/pom.xml' (see line #36 of azure-pipeline.yml file.)
   Sava and Run (Saving will commit azure-pipelines.yml to your repository in GitHub)
   Build start
   Deploy start
   Complete
   Get appservice URL/mywebapp --paste in browser---you will see web content. 
   
8] Update source code and see pipeline trigger and web content change 
   
