# ICp-banking-microservices
ICp Banking Microservices code pattern with LinuxONE Community Cloud

# Step 1 - Discover and locally run a banking application (Node.js) from a the git repository
(DOWNLOAD THE ZIP OR FORK THE REPO?!)

# Step 2 - Build and deploy a docker image from this application using a docker file to ICP (worker node on Linux on Z)

## Part 1 - Create your GitHub repository (TO MOVE TO STEP 1?)
1. Connect to your GitHub account or create one, it's free! Your username will be **YOUR_USERNAME**
2. Create a new repository and name it `icp-code-pattern-YOUR_USERNAME` (OR FORK THE REPO?!), this will be **YOUR_REPOSITORY_NAME**

## Part 2  - Validate the code and prepare the Docker image
1. On your development system, install **Node.js** and **NPM**, and the **Git CLI**

(CLONE THE REPO?! with `git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME`)

2. Make sure the app is working: (TO MOVE TO STEP 1?)
    - Go to your repository root folder:

    `cd YOUR_REPOSITORY_NAME`

    - From the app root folder, launch the app:

    `node banking-application/app.js`
    
    - If it works without any issue, stop the server with a **SIGINT (CTRL+C)**.

3. Modify the Dockerfile
    - (Steps to create the dockerfile...)

4. Push your code to your Git repository
    - Commit your changes:

    `git add .`
    `git commit -m "my message"`
    
    - Push your changes:

    `git push`

## Part 3 - Pull the code and deploy the app
1. Connect to the ICP Worker Node

2. Clone your repository
    - From the folder where you want your projet to be cloned:
    
    `git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME`

3. Build the docker image
    - Go inside the app folder:
    
    `cd YOUR_REPOSITORY_NAME/banking-application`
    
    - Build the image:
    
    `docker build -t banking-application-YOUR_USERNAME:latest .`

# Step 3 - Build and deploy an Helm chart to the ICP catalog

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

# Step 4 - Instantiate a banking microservice (from his docker image) using the ICP catalog

## Part 1 - Connect to ICP
1. Connect to the ICP Web UI through your Web browser, on **ICP_MASTER_NODE:PORT**

2. When prompted, type in these credentials then :
    - Username: `admin`
    - Password: `admin`

## Part 2 - Find and deploy your Helm chart
1. Click on the top-left *hamburger* icon, then select the **Catalog** option

2. Right to the catalog search bar, click on **???** then on the **local-charts** checkbox

3. Search for your chart named **helm-chart-YOUR_USERNAME** and click on its card

4. Bottom-right on your Helm chart page, click **configure**

5. When prompted, use `banking-application-YOUR_USERNAME` as your deployment name and select **default** as the namespace

6. Scroll down to the bottom and click the ??? button. When the process is finished, click ???

## Part 3 - Use your app
1. Scroll down and select the only **pod** available 

2. Go to your deployment

3. Select **access http** and enjoy your new app!