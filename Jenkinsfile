pipeline {
    agent any
    stages {
        stage('CI-dock'){
            parallel {
                stage('frontend') {
                    steps {
                        script {
                        sh ''' 
                            ls
                            # cd src/frontend/Dockerfile
                            docker build -f src/frontend/Dockerfile -t public.ecr.aws/y5w7f2k8/sd5184_msa_frontend:latest .
                            # aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws
                            # docker push public.ecr.aws/y5w7f2k8/sd5184_msa_frontend
                            '''
                        }
                    }
                }
                stage('backend') {
                    steps {
                        script {
                        sh ''' 
                            # cd src/backend/Dockerfile
                            # docker build -t public.ecr.aws/y5w7f2k8/sd5184_msa_backend:latest
                            # aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws .
                            # docker push public.ecr.aws/y5w7f2k8/sd5184_msa_backend
                            '''
                        }
                    }
                }

                
                

                
                
            }
        }
    }
}
