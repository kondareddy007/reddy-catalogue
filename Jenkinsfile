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
                    
                }
            }
        }
        stage(' Install Dependencies') { 
            steps {
                sh """
                npm install
                """
            }
        }
        stage('Build') { 
            steps {
            sh """
            ls -al
            zip -q -r catalogue.zip ./* -x ".git" -x "*.zip"
            ls -al
            """
            }
        }
    }
}



//nexus:-
//systemctl status nexus
//watch netstat -lntp
//labauto
//less /home/nexus/sonatype-work/nexus3/log/nexus.log
//repository creation in nexus
//admin-->account-->settings-->repositories-->create repository
//Google--> Zip files and folders in linux excluded file
// zip -r catalogue.zip ./* -x ".git" -x "*.zip" --> x means exclude files 
//Google --> silent zip in pipeline
//zip -q -r catalogue.zip ./* -x ".git" -x "*.zip"
//Google--> Delete directory in pipeline
 // deleteDir() -->add this in post() section in pipeline