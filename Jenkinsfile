pipeline {
    agent any
    stages {
        stage('CI-dock'){
            parallel {
                stage('Build and push') {
                    steps {
                        script {
                        sh ''' 
                            aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws
                            docker push public.ecr.aws/y5w7f2k8/sd5184_msa
                            '''
                        }
                    }
                }

                
                

                
                
            }
        }
    }
}
