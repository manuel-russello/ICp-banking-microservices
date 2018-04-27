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

* [IBM Cloud private](https://www.ibm.com/cloud/private)
* [IBM API Connect](http://www-03.ibm.com/software/products/en/api-connect)
* [IBM z/OS Connect Enterprise Edition](https://www.ibm.com/us-en/marketplace/connect-enterprise-edition)
* [IBM CICS Tansaction Server](https://www.ibm.com/us-en/marketplace/cics-transaction-server#product-header-top)
* [IBM Db2](https://www.ibm.com/analytics/db2/zos)

# Featured technologies

* [Docker](https://www.docker.com/)
* [Microservice](https://www.ibm.com/cloud/garage/architectures/microservices/)
* [IBM LinuxOne](https://www.ibm.com/it-infrastructure/linuxone)
* [IBM Z Mainframe](https://www.ibm.com/it-infrastructure/z)

# Steps

<!-- https://ecotrust-canada.github.io/markdown-toc/ -->

### Step 1 - Discover and locally run the banking application

- [Part 1 - Discover the banking application](#part-1---discover-the-banking-application)
- [Part 2 - Subscribe to the banking API through the API Developer Portal](#part-2---subscribe-to-the-banking-api-through-the-api-developer-portal)
- [Part 3 - Run the banking application with Node.js](#part-3---run-the-banking-application-with-nodejs)
- [Part 4 - Push the banking application to your GitHub repository](#part-4---push-the-banking-application-to-your-github-repository)

### Step 2 - Build and deploy a docker image to IBM Cloud private

- [Part 1 - Build the Docker image](#part-1---build-the-docker-image)
- [Part 2 - Deploy the docker image to IBM Cloud private](#part-2---deploy-the-docker-image-to-ibm-cloud-private)

### Step 3 - Build and deploy an Helm chart to the IBM Cloud private catalog

- [Part 1 - Create the Helm chart](#part-1---create-the-helm-chart)
- [Part 2 - Configure the Helm chart](#part-2---configure-the-helm-chart)
- [Part 3 - Package and deploy your Helm chart to the IBM Cloud private catalog](#part-3---package-and-deploy-your-helm-chart-to-the-ibm-cloud-private-catalog)

### Step 4 - Instantiate the banking microservice from the IBM Cloud private catalog

- [Part 1 - Discover your Helm chart from the calalog](#part-1---discover-your-helm-chart-from-the-calalog)
- [Part 2 - Configure and install your banking microservice](#part-2---configure-and-install-your-banking-microservice)
- [Part 3 - Access your banking microservice](#part-3---access-your-banking-microservice)

---

# Step 1 - Discover and locally run the banking application

The objective is to discover the banking application located in the *banking-application* folder. This application is a NodeJS application. It will be locally tested before packaging it into a Docker image for IBM Cloud private.

## Part 1 - Discover the banking application

1. Install the [Git command line interface](https://git-scm.com/book/en/v2/Getting-Started-The-Command-Line)

2. Launch a terminal and clone this GitHub repository:
    `git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME`

2. TODO


## Part 2 - Subscribe to the banking API through the API Developer Portal

1.	Sign up for an [IBM ID] if you don't have one already.

2.	Go to the [API Developer Portal].

3. Create an account if you have not done that already.
	![alt text](images/createAccount.png "Create Account")
   * Click **Create an Account**.
   * Provide all required information. Be sure to use your IBM ID (email address) for this account.
   * Click **Submit**.

  
   An account activation email will be sent to your registered IBM ID email. Click on the link in this email to activate your account.

4. Login to your account.

5. Create a new application.
	![alt text](images/createApplication.png "Create Application")
	* Click **Apps** from the menu.
	* Click **Create new App**.
	* Fill in all required fields.
	* Click **Submit**.
	
	Make a note of the *client ID* and *client Secret*. You will need them to access the API later.
	![alt text](images/keyApplication.png "API Keys")


6.	Before working with the banking API, you need to subscribe to it first. Display the list of available API products.
	![alt text](images/bankingProduct.png "Choose the default plan")
	* Click **API Products** from the top menu.
	* Click **Banking Product** in the list.

7. 	Subscribe to the Banking API.
	![alt text](images/APISubscription.png "Subscribe")
	* Click **Subscribe** to the Default Plan.
	
	![alt text](images/APISubscription2.png "Banking Product")
	* Select the App that you have just created before.
	* Click **Subscribe**.
	
8. Modify the *banking-application/js/bankingAPI.js* in your banking application.
	![alt text](images/client_id_secret.png "javascript code")
	* Replace *YOUR_CLIENT_ID_HERE* by your client ID value from the IBM API developer portal.
	* Replace *YOUR_CLIENT_SECRET_HERE* by your client Secret value from the IBM API developer portal.

## Part 3 - Run the banking application with Node.js

1. Install components for your environment (Windows, Mac OS, Linux):
	*	[Node.js](https://nodejs.org/en/) : Node.js is javascript server and will run the banking application. 
	* 	[npm](https://www.npmjs.com/get-npm) : npm resolves Node.js package dependencies. According to your operating system, npm may be distributed with Node.js.

2. Launch a terminal. Go to your repository root folder:

    `cd YOUR_REPOSITORY_NAME`

    - From the app root folder, launch the app:

    `node banking-application/app.js`

3. Launch a web browser and go to **localhost:3000**. The banking application appears.
    
	![alt text](images/banking_app.png "Banking application")

4. Test your application.

	![alt text](images/banking_app_test.png "Banking application")
    * Select a customer ID.
    * Please wait during the application calls banking data from the Mainframe through API Connect and z/OS Connect EE.
    * The result is displayed in a JSON structure.
    
4. The banking application locally works, stop the Node.js server with a **SIGINT (CTRL+C)** from the terminal.


## Part 4 - Push the banking application to your GitHub repository
1. Connect to your GitHub account or create one, it's free! Your username will be **YOUR_USERNAME**
2. Create a new repository and name it `icp-code-pattern-YOUR_USERNAME` (OR FORK THE REPO?!), this will be **YOUR_REPOSITORY_NAME**
3.TODO



# Step 2 - Build and deploy a docker image to IBM Cloud private

The objective is to build a docker image from the banking application and then deploy it to the IBM Cloud private.

## Part 1 - Build the Docker image

1. Push your code to your Git repository
    - Commit your changes:

    `git add .`
    `git commit -m "my message"`
    
    - Push your changes:

    `git push`

## Part 2 -  Deploy the docker image to IBM Cloud private
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

The objective is to build ...


## Part 1 - Create the Helm chart
1. Go back to your development system

2. Create your helm chart   
    `helm create helm-chart-YOUR_USERNAME`

3. Go to your chart folder
    `cd helm-chart-YOUR_USERNAME`

## Part 2 - Configure the Helm chart
(Steps to create the files and configure the values)

10. Validate the Helm chart:
    - Go to the parent folder:
    
    `cd ..`

    - Analyse and validate the chart:
    `helm lint helm-chart-YOUR_USERNAME`

## Part 3 - Package and deploy your Helm chart to ICP
1. Package the Helm chart
    
    `helm package helm-chart-YOUR_USERNAME`

2. Connect to ICP
    - Execute this command:

    `bx pr login -a https://MASTER_NODE_IP:PORT --skip-ssl-validation`
    
    - When prompted, type in these credentials:
        - Username: `admin`
        - Password: `admin`
        - Select an account: `1`
 
3. Upload the package to ICP
    `bx pr load-helm-chart --archive helm-chart-YOUR_USERNAME-0.1.0.tgz --clustername MASTER_NODE_IP`

# Step 4 - Instantiate the banking microservice from the IBM Cloud private catalog

The objective is to ...


## Part 1 - Discover your Helm chart from the calalog
1. Connect to the ICP Web UI through your Web browser, on **ICP_MASTER_NODE:PORT**

2. When prompted, type in these credentials then :
    - Username: `admin`
    - Password: `admin`

3. Click on the top-left *hamburger* icon, then select the **Catalog** option

4. Right to the catalog search bar, click on **Filter** then on the **local-charts** checkbox

5. Search for your chart named **helm-chart-YOUR_USERNAME** and click on its card

## Part 2 - Configure and install your banking microservice

1. Bottom-right on your Helm chart page, click **configure**

2. When prompted, use `banking-application-YOUR_USERNAME` as your release name and select **default** as the target namespace

3. Scroll down to the bottom and click the **Install** button. When the process is finished, click **View Helm Release**

## Part 3 - Access your banking microservice
1. Scroll down and click on the only **deployment** available 

2. Select **access http** under the **Expose details** panel and enjoy your new app!

#Troubleshooting
#Privacy Notice
#Links


[IBM ID]: https://www.ibm.com/account/us-en/signup/register.html
[API Developer Portal]: https://developer-contest-spbodieusibmcom-prod.developer.us.apiconnect.ibmcloud.com/
