# HOL-Devops

In this labs you will implement an example of continuous build and deployment of containerized Java Web applications using Linux, Maven, Tomcat, Jenkins, Docker and Eclipse on Azure; this is a classic DevOps scenario and here you will learn how to build a DevOps lifecycle from scratch.

## Before you begin this lab

Before you begin this hands on lab, you need to make sure you have: An Azure account. 

If you don't have one already, you can create [a free Azure account today](https://azure.microsoft.com/en-us/free/).

## Detailed contents of the HOL

 - [Introduction to the HOL-Devops ](./001-introduction.md)
    
1. [Creating and configuring a Jenkins server in Azure](./002-lab-setup.md)  
   * Overview
        * Objectives
        * Requirements
    * Creating a VM in Azure running Jenkins
    * Configuring VM's Network Interface
    * Unlock Jenkins
    * Setting up Communication between Jenkins and Docker
    * Setting up Jenkins
        * Install pluggins
        * Maven Configuration

2. [Setting up an automated Build and Deploy in Jenkins server in Azure](./003-jenkins-build-deploy.md)  
    * Overview
        * Objectives
        * Requirements
    * Creating a Build project
    * Creating a Deployment project
    * Running the project
