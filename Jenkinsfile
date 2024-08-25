pipeline {
    agent any

    environment {
        AWS_CREDENTIALS = credentials('90eb4d03-9c24-4e7d-b4f9-426760a790a8')
        ECR_REPO_URI = "public.ecr.aws/y5w7f2k8/sd5184_msa"
        IMAGE_TAG = "hello-world:${env.BUILD_ID}"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo/hello-world.git'
            }
        }

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
                    withAWS(credentials: '90eb4d03-9c24-4e7d-b4f9-426760a790a8', region: 'us-east-1') {
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
