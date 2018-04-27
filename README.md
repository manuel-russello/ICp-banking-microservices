# Title

In this Code Pattern, we will build and deploy microservices using IBM Cloud private and the LinuxONE Community Cloud. [Explain briefly how things work]. [Give acknowledgements to others if necessary]

When the reader has completed this Code Pattern, they will understand how to:

* [goal 1]
* [goal 2]
* [goal 3]
* [goal 4]

<!--Remember to dump an image in this path-->
![](doc/source/images/architecture.png)

## Flow
<!--Add new flow steps based on the architecture diagram-->
1. Step 1.
2. Step 2.
3. Step 3.
4. Step 4.
5. Step 5.

<!--Update this section-->
## Included components
Select components from [here](https://github.ibm.com/developer-journeys/journey-docs/tree/master/_content/dev#components), copy and paste the raw text for ease
* [Component](link): description
* [Component](link): description

<!--Update this section-->
## Featured technologies
Select components from [here](https://github.ibm.com/developer-journeys/journey-docs/tree/master/_content/dev#technologies), copy and paste the raw text for ease
* [Technology](link): description
* [Technology](link): description

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