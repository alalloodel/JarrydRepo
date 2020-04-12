# Serverless Web App Hosted on AWS Starter Kit

## Intention

- Enable anyone to launch and begin developing a web app
- Includes an Azure pipeline which will deploy the front-end to an S3 bucket and create the following AWS services:
- API gateway
- Sample Lambda Function

# Getting Started - Pre-requisits

1. Install Node.js (https://nodejs.org/en/download/)
2. Install Python (https://www.python.org/downloads/ ensure you add Python to PATH)
3. Install Serverless (Serverless guide: https://serverless-stack.com/)
```bash
npm install -g serverless
```

# Getting Started - Front-end

Replace the sample web app in the frontend folder with yours, or use the provided starter:

The starter project was taken from the Git project (https://github.com/tomastrajan/angular-ngrx-material-starter) and includes an Angular 8 starter with material ui library

1. Go to project folder (frontend/sample-web-app-angular-material) and install dependencies:
```bash
npm install
```

2. Launch development server, and open `localhost:4200` in your browser:
```bash
npm start
```

# Getting Started - Back-End

## Installing AWS Extensions in Azure

- Go to organisation settings (Fig. 1)
- Go to Extensions (Fig. 2)
- Browse the marketplace
- Install AWS extension, if you are not the organisational owner, they will be sent a request to approve the installation.

![org-settings](meta-assets/guide-aws-toolkit-org-settings.png)
<p align=center> Figure 1: Azure Organisation Settings

![marketplace](meta-assets/guide-aws-toolkit-marketplace-search.png)
<p align=center> Figure 2: AWS Toolkit Extension

## Files to update

### azure-pipelines.yaml

For the pipeline to deploy, you will need to create a few pipeline variables:

- $(env.AWS_CREDENTIALS_PROFILE_NAME): The profile setup with your AWS credentials in Azure
- $(env.AWS_DEPLOYMENT_REGION): The region in which you want to deploy your web app
- $(env.AWS_DEPLOYMENT_BUCKET): The bucket that is created to deploy your web app - must match your web app bucket name *(webAppBucketName variable in serverless/resources/storage/serverless.yml)*.
- $(env.AWS_DEPLOYMENT_STAGE): The stage of your deployment

### serverless/resources/storage/serverless.yml

- projectCode: Create a project code (ensure that it will be unique as it affects S3 deployment bucket)
- webAppBucketName: defaults to projectCode-website

## Deploying manually

1. Go to root serverless project folder (serverless) and install dependencies:
```bash
npm install
```

2. To Deploy your serverless folderto AWS, ensure CLI credentials are installed locally or in pipeline and run the deployment command (modifying parameters as required):
```bash
serverless deploy --aws-profile namedAWSCredentials --region us-east-1 --stage dev
```

3. To add additional serverless projects, copy a sample serverless folder and add the deployment command to the project folder.

4. Note that the serverless project is broken up into multiple smaller projects to alleviate some issues with circular dependencies as well as circumvent the 200 resource limit on cloudformation which is also imposed on serverless.

# Future Development

- Enable offline development and testing of lambda functions
- Improve sample lambda functions
- Add knowledge wiki