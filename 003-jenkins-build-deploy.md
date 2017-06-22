# 3 Setting up an automated Build and Deploy in Jenkins server in Azure

## 3.1 Overview
In this lab, we will setting up a build and deploy project in Jenkins.

### 3.1.1 Objectives
This lab aims to get you familiar with Jenkins on Azure Cloud.

### 3.1.2 Requirements
You must have completed Lab 01.

## 3.2 Creating a Build project
1. Go to the Jenkins Dashboard and click on "New Item".

2. Create a "Freestyle project" with the name "build" and click "OK" to continue.
    ![](./images/3.1.i001.PNG)

3. Configure the Github project and the Source Code Managment with your repository. For this lab we will use **https://github.com/karolikl/hol-oss-devops.git/**

    ![](./images/3.1.i002.PNG)
    
    ![](./images/3.1.i003.PNG)
    
4. Click on the "Build" tab of the configuration. In the "Add build step" dropdown, select "Invoke top-level Maven targets".
    
   ![](./images/3.1.iu004.PNG)

   Click on the arrow next to the "Goals" textbox to expand the textbox to multiple lines. 
  
   Select the "Maven Version" we set up previously and specify the following goals for the build and click on the "Advanced..." button:
    ```
    clean
    package
    ``` 
   Add the following "POM" file path to the configuration:
    ```
    sample-app/pom.xml //configure with your path
    ```

5. Click on the "Build" tab of the configuration. In the "Add build step" dropdown, select "Exetute shell".
  
   In the Command section and add 
   
    ```
    docker run -it --name your_container_name -d -p 8888:8080 tomcat:8.0
    ``` 
       
6. Click on the "Post-build Actions" tab and add a post-build action of type "Archive the artifact" where you archive the files matching the following pattern:
    ```
    **/target/*.war
    ``` 
    ![](./images/3.1.i005.PNG)

7. Click on "Save".


## 3.3 Creating a Deployment project
1. Go to the Jenkins Dashboard and click on "New Item".

2. Create a "Freestyle project" with the name "Deploy" and click "OK" to continue.
    ![](./images/3.2.i001.PNG)
    
3. Configure the Build triggers. Select "Build after other projects are build" and configure the **project-created-in-previous-section** project

    ![](./images/3.2.i002.PNG)
    
4. Click on the "Build" tab of the configuration. In the "Add build step" dropdown, select "Copy artifacts from another project".

   Fill the settings:  
   **Project name:** your project name  
   **Wich version:** select Last succesfull build  
   **Artifacts to copy:** **/target/*.war  
   **Target directory:** $WORKSPACE  

    ![](./images/3.2.i003.PNG)

5. Click on the "Build" tab of the configuration. In the "Add build step" dropdown, select "Exetute shell".
  
   In the Command section and add 
   
    ```
       docker cp  /var/lib/jenkins/workspace/build/sample-app/target/OSSDevOpsHOL.war your_container_name:/usr/local/tomcat/webapps/OSSDevOpsHOL.war'

    ``` 
    ![](./images/3.2.iu004.PNG)

6. Click on "Save".

## 3.4 Running the Project

1. Run the build project to start the flow
2. Once the build and deploy finish browse to http://yourazurevmip:8888/OSSDevOpsHOL
![](./images/3.2.i005.PNG)