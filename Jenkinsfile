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
                def packageJson = readJson file: 'package.json'
                    packageVersion = packageJson.version
                    echo "Application version is: $packageVersion"
                    echo "Application details is: $packageJson"
                    
                }
            }
        }
        stage('Test') { 
            steps {
                echo "hello" 
            }
        }
        stage('Deploy') { 
            steps {
                echo "hello" 
            }
        }
    }
}