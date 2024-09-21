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
                    sh 'npm config set registry https://registry.npmmirror.com/'
                    sh 'npm i newman '
                    sh 'npm i newman-reporter-htmlextra'
                    sh 'newman --version'
                    sh 'newman-reporter-htmlextra --version'
                    sh 'pwd'
                    sh 'ls'
                }
            }
        }  
    }
}