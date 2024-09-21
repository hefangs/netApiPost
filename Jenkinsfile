pipeline {
    agent any
    stages {
        stage('Install Node') {   
            steps {
                withDockerContainer('node') {
                    sh 'node -v'
                    sh 'npm -v'
                    sh 'pwd'
                    sh 'ls'
                }
            }
        }  
    }
}