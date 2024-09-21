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
                    sh 'npm config set registry https://registry.npm.taobao.org'
                    sh 'npm i newman '
                    sh 'npm i newman-reporter-htmlextra'
                    sh 'newman -v'
                    sh 'newman-reporter-htmlextra -v'
                }
            }
        }  
    }
}