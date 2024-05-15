# CI/CD Pipeline for Dockerized Flask Application on AWS EC2

This repository contains code for setting up a Continuous Integration and Continuous Deployment (CI/CD) pipeline for a Dockerized Flask application on AWS EC2 using Jenkins. The pipeline automates the building, testing, and deployment processes for the application.

## Prerequisites

- AWS account
- Jenkins installed and configured on an EC2 instance
- Docker installed on the Jenkins EC2 instance
- Git installed on the Jenkins EC2 instance

## Step 1: Launch an EC2 Instance

1. Log in to the AWS Management Console.
2. Navigate to the EC2 dashboard.
3. Click on "Launch Instance" and choose an Amazon Linux AMI.
4. Select an instance type, configure instance details, add storage, and configure security groups to allow inbound traffic on port 22 (SSH) and port 80 (HTTP).
5. Launch the instance and create a new key pair if needed. Save the private key securely.

## Step 2: Connect to the EC2 Instance

1. Once the instance is running, connect to it via SSH using the private key:

   ```bash
   ssh -i /path/to/private-key.pem ec2-user@<instance-public-ip>
   ```

## Step 3: Install Jenkins, Docker, and Git

1. Install Jenkins by following the official installation instructions: [Jenkins Installation Guide](https://www.jenkins.io/doc/book/installing/)
2. Install Docker by following the official installation instructions: [Docker Installation Guide](https://docs.docker.com/engine/install/)
3. Install Git:

   ```bash
   sudo yum install git
   ```

## Step 4: Clone this Repository

1. Clone this repository onto your EC2 instance:

   ```bash
   git clone https://github.com/BairojuSaidachary/CI-CD.git
   ```

## Step 5: Configure Jenkins

1. Access Jenkins in your web browser by navigating to `http://<instance-public-ip>:8080`.
2. Follow the on-screen instructions to complete the Jenkins setup wizard.
3. Install necessary plugins including Git and Docker.
4. Create a new Jenkins pipeline job and configure it to use the `Jenkinsfile` in the cloned repository.

## Step 6: Run the Pipeline

1. Trigger the Jenkins pipeline manually or set up a webhook to trigger it automatically on code changes.
2. Jenkins will execute the pipeline, which includes:
   - Checking out the code from the GitHub repository.
   - Building the Docker image for the Flask application.
   - Pushing the Docker image to Docker Hub.
   - Optionally, deploying the application to AWS ECS, Kubernetes, or any other platform.

## Step 7: Access the Deployed Application

1. Once the pipeline is successfully executed, you can access the deployed Flask application in your web browser at `http://<instance-public-ip>:5000`.

## About the Application

The Flask application is a simple "Hello, World!" web service. It exposes a single endpoint at `/` that returns a greeting message.

## Dependencies

- Flask==2.0.2
- Werkzeug==2.2.2

## Author

@Saidachary

