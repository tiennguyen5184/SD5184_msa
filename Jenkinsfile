pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
               script {
                sh 'whoami'
                sh 'docker ps'
               }
            }
        }
    }
}
