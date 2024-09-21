pipeline {
    agent any
    stages {
        stage('Pytest Testcases') {   
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