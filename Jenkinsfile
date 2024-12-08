pipeline {
    agent {
        node {
            label 'AGENT'
        }
    } 
    environment {
        packageVersion = ''
    }

    stages {
        stage('Get the version') { 
            steps {
                script{
                def packageJson = readJson file: 'package.json'
                    packageVersion = packageJson.version
                    
                }
            }
        }
        stage('Test') { 
            steps {
                // 
            }
        }
        stage('Deploy') { 
            steps {
                // 
            }
        }
    }
}