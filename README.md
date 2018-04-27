# Create and deploy a financial microservice to Linux on Z using IBM Cloud Private 

In this Code Pattern, you will build and deploy a banking microservice with IBM Cloud private running in the LinuxONE Community Cloud. 

IBM Cloud Private is a private cloud platform for developing and running workloads locally. It is an integrated environment that enables you to design, develop, deploy and manage on-premises, containerized cloud applications behind a firewall. It includes the container orchestrator Kubernetes, a private image repository, a management console and monitoring frameworks.

When you will complete this Code Pattern, you will understand how to:

* Build a Docker image from an existing application.
* Deploy a Docker image to IBM Cloud Private.
* Deploy a Helm chart.
* Use the catalog from IBM Cloud Private.

# Architecture

This journey accesses a fictitious retail banking system called MPLbank. MPLbank integrates an Account Management System running on IBM Mainframe. On top of this component, an API layer based on IBM API Connect has been set up to deliver a banking API. It makes banking services reachable through API from all kind of applications. IBM Cloud private has been configured into the LinuxOne LinuxONE Community Cloud.

![alt text](images/architecture_pattern.png "Architecture")

1. The user deploys the application based microservice on the worker Node on Linux on Z using IBM Cloud Private.
2. The user installs and runs an instance of his microservice from IBM Cloud Private. The application calls a banking API published in API Connect.
3. API Connect calls the back-end Z Mainframe through a banking API published in z/OS Connect EE.
4. z/OS Connect EE calls the Account Management System (AMS) running in CICS. A COBOL program processes the request and returns banking data. Finally, banking data are sent back to microservice application in the Worker Node on Linux on Z.


# Included components

* [IBM LinuxOne](https://www.ibm.com/it-infrastructure/linuxone)
* [IBM Cloud Private](https://www.ibm.com/cloud/private)
* [IBM Z Mainframe](https://www.ibm.com/it-infrastructure/z)
* [IBM z/OS Connect Enterprise Edition](https://www.ibm.com/us-en/marketplace/connect-enterprise-edition)
* [IBM CICS Tansaction Server](https://www.ibm.com/us-en/marketplace/cics-transaction-server#product-header-top)
* [IBM Db2](https://www.ibm.com/analytics/db2/zos)

# Featured technologies

* [microservice](https://www.ibm.com/cloud/garage/architectures/microservices/)
* [IBM LinuxOne](https://www.ibm.com/it-infrastructure/linuxone)
* [IBM Cloud Private](https://www.ibm.com/cloud/private)

# Steps

# Step 1 - Discover and locally run a banking application (Node.js) from a the git repository

## Part 1 - Discover the banking application

## Part 2 - Subscribe to the API through API Connect

## Part 3 - Create your GitHub repository (TO MOVE TO STEP 1?)
1. Connect to your GitHub account or create one, it's free! Your username will be **YOUR_USERNAME**
2. Create a new repository and name it `icp-code-pattern-YOUR_USERNAME` (OR FORK THE REPO?!), this will be **YOUR_REPOSITORY_NAME**

## Part 4  - Validate the code and locally run the app
1. Log in onto your development system, then install **Node.js**, **NPM**, and the **Git CLI**

## Step 2 - Build and deploy a docker image from this application using a docker file to ICP (worker node on Linux on Z)

### Part 1 - Create your GitHub repository (TO MOVE TO STEP 1?)
1. Connect to your GitHub account or create one, it's free! Your username will be **YOUR_USERNAME**
2. Create a new repository and name it `icp-code-pattern-YOUR_USERNAME` (OR FORK THE REPO?!), this will be **YOUR_REPOSITORY_NAME**

### Part 2  - Validate the code and prepare the Docker image
1. On your development system, install **Node.js** and **NPM**, and the **Git CLI**

2. Clone your GitHub repository:
    `git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME`

3. Make sure the app is working: (TO MOVE TO STEP 1?)
    - Go to your repository root folder:

    `cd YOUR_REPOSITORY_NAME`

    - From the app root folder, launch the app:

    `node banking-application/app.js`
    
    - If it works without any issue, stop the server with a **SIGINT (CTRL+C)**.

# Step 2 - Build and deploy a docker image from this application using a docker file to ICP (worker node on Linux on Z)

## Part 1 - Prepare the Docker image

1. Push your code to your Git repository
    - Commit your changes:

    `git add .`
    `git commit -m "my message"`
    
    - Push your changes:

    `git push`

## Part 2 - Pull the code and deploy the app
1. Connect to the ICP Worker Node

2. Clone your repository
    - From the folder where you want your projet to be cloned:
    
    `git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME`

3. Build the docker image
    - Go inside the app folder:
    
    `cd YOUR_REPOSITORY_NAME/banking-application`
    
    - Build the image:
    
    `docker build -t banking-application-YOUR_USERNAME:latest .`

    This step will build a **Docker image** and host it on the Worker Node's image repository, according to the steps written in the **Dockerfile**.

# Step 3 - Build and deploy an Helm chart to the ICP catalog

### Part 1 - Create the Helm chart
1. Go back to your development system

2. Create your helm chart   
    `helm create helm-chart-YOUR_USERNAME`

3. Go to your chart folder
    `cd helm-chart-YOUR_USERNAME`

### Part 2 - Configure the Helm chart
(Steps to create the files and configure the values)

10. Validate the Helm chart:
    - Go to the parent folder:
    
    `cd ..`

    - Analyse and validate the chart:
    `helm lint helm-chart-YOUR_USERNAME`

### Part 3 - Package and deploy your Helm chart to ICP
2. Package the Helm chart
    
    `helm package helm-chart-YOUR_USERNAME`

3. Connect to ICP
    - Execute this command:

    `bx pr login -a https://MASTER_NODE_IP:PORT --skip-ssl-validation`
    
    - When prompted, type in these credentials:
        - Username: `admin`
        - Password: `admin`
        - Select an account: `1`
 
4. Upload the package to ICP
    `bx pr load-helm-chart --archive helm-chart-YOUR_USERNAME-0.1.0.tgz --clustername MASTER_NODE_IP`

## Step 4 - Instantiate a banking microservice (from his docker image) using the ICP catalog

### Part 1 - Connect to ICP
1. Connect to the ICP Web UI through your Web browser, on **ICP_MASTER_NODE:PORT**

2. When prompted, type in these credentials then :
    - Username: `admin`
    - Password: `admin`

### Part 2 - Find and deploy your Helm chart
1. Click on the top-left *hamburger* icon, then select the **Catalog** option

2. Right to the catalog search bar, click on **Filter** then on the **local-charts** checkbox

3. Search for your chart named **helm-chart-YOUR_USERNAME** and click on its card

4. Bottom-right on your Helm chart page, click **configure**

5. When prompted, use `banking-application-YOUR_USERNAME` as your release name and select **default** as the target namespace

6. Scroll down to the bottom and click the **Install** button. When the process is finished, click **View Helm Release**

## Part 3 - Use your app
1. Scroll down and click on the only **deployment** available 

2. Select **access http** under the **Expose details** panel and enjoy your new app!

#Troubleshooting
#Privacy Notice
#Links