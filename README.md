# Deploy Python Application on AWS

This project automates the deployment of a Python application using GitHub Actions to AWS instances with Docker containers.

The workflow covers building the Docker image, pushing it to Docker Hub, and deploying it to AWS EC2 instances for both *QA* and *Main* environments.

## Table of Contents
- [Prerequisites](#prerequisites)
- [CI/CD Workflow](#cicd-workflow)
- [Deployment Steps](#deployment-steps)
  - [Deploy to QA Environment](#deploy-to-qa-environment)
  - [Deploy to Main Environment](#deploy-to-main-environment)
- [Environment Variables](#environment-variables)
- [Dependencies Installation](#dependencies-installation)
- [Contributing](#contributing)

## Prerequisites

Before you begin, ensure you have the following:

- *Docker*: Required for building and running Docker images.
- *AWS EC2*: Two EC2 instances (one for the QA environment and another for the Main environment) should be set up and ready to deploy.
- *GitHub Secrets*: Ensure you have the appropriate SSH keys and Docker credentials configured in GitHub secrets.

## CI/CD Workflow

This workflow is automated using GitHub Actions and consists of three main stages:

### 1. *Build Docker Image*
When a push is made to the qa or main branches, the workflow builds a new Docker image tagged with the branch name (qa or main), and then pushes it to Docker Hub.

### 2. *Deploy to AWS EC2*
The workflow deploys the application to the respective EC2 instance depending on the branch that was pushed:
- If the push is to the qa branch, it deploys to the QA EC2 instance.
- If the push is to the main branch, it deploys to the Main EC2 instance.

## Deployment Steps

### Deploy to QA Environment

1. *Set up SSH Key*: The SSH key for the QA instance is set up from GitHub secrets.
2. *SSH Connection to EC2 Instance*: Connects to the QA EC2 instance via SSH.
3. *Install Docker*: If Docker is not installed, the script installs it automatically.
4. *Deploy Docker Image*: The Docker image is pulled from Docker Hub and run on the EC2 instance, exposing port 5000.

### Deploy to Main Environment

1. *Set up SSH Key*: The SSH key for the Main instance is set up from GitHub secrets.
2. *SSH Connection to EC2 Instance*: Connects to the Main EC2 instance via SSH.
3. *Install Docker*: If Docker is not installed, the script installs it automatically.
4. *Deploy Docker Image*: The Docker image is pulled from Docker Hub and run on the EC2 instance, exposing port 5000.

## Environment Variables

The workflow uses several environment variables and GitHub secrets that need to be configured:

- *DOCKER_USERNAME*: Docker Hub username for authentication.
- *DOCKER_PASSWORD*: Docker Hub password for authentication.
- *QA_SSH_KEY*: SSH private key for accessing the QA EC2 instance.
- *MAIN_SSH_KEY*: SSH private key for accessing the Main EC2 instance.

## Dependencies Installation

If you need to run or modify this workflow locally, ensure the following dependencies are installed:

1. *Docker*: Installed and configured on your local machine for building the Docker image.
2. *GitHub CLI*: If you need to interact with GitHub secrets or test the workflow locally.
3. *AWS CLI*: To interact with the EC2 instances and manage the AWS environment if needed.

## Contributing

1. *Fork the repository*.
2. *Create a branch*: git checkout -b feature/my-new-feature.
3. *Make your changes*.
4. *Commit your changes*: git commit -am 'Add new feature'.
5. *Push to your branch*: git push origin feature/my-new-feature.
6. *Create a Pull Request*.

---

This README.md provides an overview of the CI/CD workflow that automates building and deploying a Python application in Docker containers to AWS EC2 instances using GitHub Actions.
