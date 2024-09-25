pipeline {
    agent any
    stages {
        // stage('Build Docker Image') {
        //     steps {
        //         script {
        //             docker.build("hello-world:")
        //         }
        //     }
        // }

        
        stage('Login to ECR') {
            steps {
                script {
                   sh ''' 
                       aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws
                    '''
                }
            }
        }

        stage('Tag image') {
            steps {
                script {
                    sh '''
                        echo $USER
                        sudo usermod -aG docker $USER
                        newgrp docker
                        docker tag hello-world public.ecr.aws/y5w7f2k8/sd5184_msa/helloword:latest
                    '''
                }
            }
        }
        stage('Push image'){
            steps{
                script{
                    sh '''
                        docker push public.ecr.aws/y5w7f2k8/sd5184_msa/helloword:latest
                    '''
                }
            }
        }
    }
}
