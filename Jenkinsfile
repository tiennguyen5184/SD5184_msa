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
                    docker.build("hello-world:${IMAGE_TAG}")
                }
            }
        }

        stage('Login to ECR') {
            steps {
                script {
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', 
                                      credentialsId: 'aws-credentials', 
                                      accessKeyVariable: 'AWS_ACCESS_KEY_ID', 
                                      secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                        sh 'aws ecr get-login-password --region region | docker login --username AWS --password-stdin ${ECR_REPO_URI}'
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
