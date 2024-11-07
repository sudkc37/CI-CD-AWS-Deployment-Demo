The workflow outlines a CI/CD pipeline using GitHub Actions with Docker, ECR, and EC2 for continuous integration and deployment of very simple application.
## WorkFlow Explaination:

## Basic Workflow:
1. The workflow starts automatically when code is pushed to the main branch, except when only the README.md file is changed.
2. The workflow uses GitHub's permissions to allow it to read the repository and manage AWS authentication.
## Continuous Integration (CI) Stage:
3. GitHub Actions checks out the latest code from the repository to ensure all steps are working with the current version.
4. The workflow runs a linting step to check for any syntax or style issues in the code.
5. The workflow executes unit tests to verify that individual parts of the code are functioning correctly.
## Continuous Delivery (CD) Stage:
6. Essential utilities like jq and unzip are installed, if needed, for the build process.
7. AWS credentials are configured using GitHub Secrets to authenticate with Amazon services.
8. GitHub Actions authenticates with Amazon Elastic Container Registry (ECR) to allow Docker images to be pushed.
9. The Docker image is built from the code and tagged with the latest label.
10. The built Docker image is pushed to ECR, making it available for deployment.
## Continuous Deployment Stage: 
11. The EC2 instance pulls the latest Docker image from Amazon ECR.
12.  If an existing container with the same name is running, it is stopped and removed to prevent conflicts.
13.  The new Docker container is launched on the EC2 instance, making the application available to users. AWS credentials and configuration are passed as environment variables for seamless operation.
14.  Unused Docker images and containers are removed to free up disk space on the EC2 instance.
    
AWS SetUP:

## 1. Login to AWS console.

## 2. Create IAM user for deployment

	with specific access
	1. EC2 access : It is virtual machine

	2. ECR: Elastic Container registry
	To save your docker image in aws

	Description: About the deployment

	1. Build docker image of the source code
	2. Push your docker image to ECR
	3. Launch Your EC2 
	4. Pull Your image from ECR in EC2
	5. Lauch your docker image in EC2

	Policy:
	1. AmazonEC2ContainerRegistryFullAccess
	2. AmazonEC2FullAccess

	
## 3. Create ECR repo to store/save docker image
    - Save the URI: 315865595366.dkr.ecr.us-east-1.amazonaws.com/your reponame

	
## 4. Create EC2 machine (Ubuntu) 

## 5. Open EC2 and Install docker in EC2 Machine:
	
	
	#optinal
	sudo apt-get update -y
	sudo apt-get upgrade
	
	#required
	curl -fsSL https://get.docker.com -o get-docker.sh
	sudo sh get-docker.sh
	sudo usermod -aG docker ubuntu
	newgrp docker
	
## 6. Configure EC2 as self-hosted runner:
    setting>actions>runner>new self hosted runner> choose os> 
    then run command one by one


## 7. Setup github secrets:

    AWS_ACCESS_KEY_ID=

    AWS_SECRET_ACCESS_KEY=

    AWS_REGION = us-east-1

    AWS_ECR_LOGIN_URI = demo>>  566373416292.dkr.ecr.ap-south-1.amazonaws.com

    ECR_REPOSITORY_NAME = 
