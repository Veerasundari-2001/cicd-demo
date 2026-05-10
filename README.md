# AWS CI/CD Pipeline with Jenkins, Docker & ECR

A production-style CI/CD pipeline that automatically builds, tests, and deploys a Python Flask application to AWS using Jenkins, Docker, and Amazon ECR.

## Architecture
GitHub → Jenkins (EC2) → Docker Build → Amazon ECR → App Server (EC2)

## Tech Stack

- **Cloud:** AWS EC2, Amazon ECR, IAM
- **CI/CD:** Jenkins
- **Containerization:** Docker
- **App:** Python Flask
- **Testing:** Pytest
- **Source Control:** Git & GitHub

## Pipeline Stages

1. **Build** — Installs Python dependencies
2. **Test** — Runs automated tests using Pytest
3. **Docker Build & Push** — Builds Docker image and pushes to Amazon ECR
4. **Deploy** — Pulls latest image and runs container on App Server EC2

## Project Structure
cicd-demo/
├── app.py              # Flask application
├── test_app.py         # Unit tests
├── requirements.txt    # Python dependencies
├── Dockerfile          # Container configuration
└── Jenkinsfile         # Pipeline definition

## Infrastructure Setup

- **Jenkins Server** — EC2 t2.micro (Ubuntu 22.04) with Jenkins, Docker, AWS CLI
- **App Server** — EC2 t2.micro (Ubuntu 22.04) with Docker, AWS CLI
- **ECR Repository** — Private Docker image registry
- **IAM Role** — EC2 role with ECR full access

## How It Works

1. Developer pushes code to GitHub
2. Jenkins pulls latest code automatically
3. Dependencies are installed and tests are run
4. Docker image is built and pushed to ECR
5. App Server pulls the latest image and restarts the container
6. App is live at `http://<APP_EC2_IP>:5000`

## Live Demo

Visit: `http://3.1.100.20:5000`

## Key Learnings

- Setting up Jenkins on AWS EC2
- Configuring IAM roles for secure ECR access
- Building and pushing Docker images to Amazon ECR
- Automating deployment using Jenkins Pipeline
- SSH-based deployment between EC2 instances
