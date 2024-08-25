pipeline {
    agent any

    environment {
        AWS_CREDENTIALS = credentials('aws-credentials')
        ECR_REPO_URI = "public.ecr.aws/y5w7f2k8/sd5184_msa"
        IMAGE_TAG = "hello-world:${env.BUILD_ID}"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${ECR_REPO_URI}:${IMAGE_TAG}")
                }
            }
        }

        stage('Login to ECR') {
            steps {
                script {
                    withAWS(credentials: 'aws-credentials', region: 'us-east-1') {
                        ecrLogin()
                    }
                }
            }
        }

        stage('Push to ECR') {
            steps {
                script {
                    docker.image("${ECR_REPO_URI}:${IMAGE_TAG}").push()
                }
            }
        }
    }
}
