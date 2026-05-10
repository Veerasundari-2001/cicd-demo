pipeline {
    agent any
    environment {
        ECR_URI = "521223133955.dkr.ecr.ap-southeast-1.amazonaws.com/cicd-demo"
        AWS_REGION = "ap-southeast-1"
        APP_SERVER = "ubuntu@3.1.100.20"
    }
    stages {
        stage('Build') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                sh 'pytest test_app.py -v'
            }
        }
        stage('Docker Build and Push') {
            steps {
                sh 'aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 521223133955.dkr.ecr.ap-southeast-1.amazonaws.com/cicd-demo'
                sh 'docker build -t cicd-demo:latest .'
                sh 'docker tag cicd-demo:latest 521223133955.dkr.ecr.ap-southeast-1.amazonaws.com/cicd-demo:latest'
                sh 'docker push 521223133955.dkr.ecr.ap-southeast-1.amazonaws.com/cicd-demo:latest'
            }
        }
        stage('Deploy') {
            steps {
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.1.100.20 "docker pull 521223133955.dkr.ecr.ap-southeast-1.amazonaws.com/cicd-demo:latest && docker stop cicd-demo || true && docker rm cicd-demo || true && docker run -d --name cicd-demo -p 5000:5000 521223133955.dkr.ecr.ap-southeast-1.amazonaws.com/cicd-demo:latest"'
            }
        }
    }
    post {
        success { echo 'Deployed!' }
        failure { echo 'Failed!' }
    }
}
