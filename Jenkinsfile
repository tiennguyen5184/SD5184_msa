pipeline {
    agent any
    stages {
        stage('CI-dock'){
            parallel {
                stage('frontend') {
                    steps {
                        script {
                        sh ''' 
                            ecr_alias=$(aws ecr-public describe-registries --region us-east-1 --query "registries[0].aliases[0].name" --output text)
                            docker build -t public.ecr.aws/y5w7f2k8/sd5184_msa_frontend:latest src/frontend/
                            aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws
                            docker push public.ecr.aws/y5w7f2k8/sd5184_msa_frontend
                            '''
                        }
                    }
                }
                stage('backend') {
                    steps {
                        script {
                        sh ''' 
                            ecr_alias=$(aws ecr-public describe-registries --region us-east-1 --query "registries[0].aliases[0].name" --output text)
                            docker build -t public.ecr.aws/y5w7f2k8/sd5184_msa_backend:latest src/backend/
                            aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws
                            docker push public.ecr.aws/y5w7f2k8/sd5184_msa_backend
                            '''
                        }
                    }
                }

                
                

                
                
            }
        }
    }
}
