pipeline {
    agent {
        node {
            label 'AGENT'
        }
    } 
    environment {
        packageVersion = ''
    }
    options {
        timeout( time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }

    stages {
        stage('Get the version') { 
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    packageVersion = packageJson.version
                    echo "application version: $packageVersion"
                    echo "application Details: $packageJson"
                }
            }
        }
        stage(' Install Dependencies') { 
            steps {
                sh """
                npm install
                ls -al
                """
            }
        }
        stage('Deploy') { 
            steps {
                sh """
                ls -al
                """
            }
        }
    }
}