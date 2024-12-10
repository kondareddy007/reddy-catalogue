pipeline {
    agent {
        node {
            label 'AGENT'
        }
    } 
    environment {
        packageVersion = ''
        nexusURL = '172.31.93.24:8081'
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
        stage('Publish artifact')
        {
            steps {
        nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: "${nexusURL}",
        groupId: 'com.roboshop',
        version: "${packageVersion}",
        repository: 'catalogue',
        credentialsId: 'nexus_auth',
        artifacts: [
            [artifactId: 'catalogue',
             classifier: '',
             file: 'catalogue.zip', 
             type: 'zip']
        ]
     )
            }
        }
        stage('Deploy') {
            steps {
                script {
                    def params = [
                         string(name: 'version', value: "${packageVersion}"),
                         string(name: 'environment', value: "dev")
                    ]
                    build job: 'catalogue-deploy', wait: true, parameters: params
                }
            }
        }
    }

    post {
        always {
            echo 'it will always say hello again'
            deleteDir()
        }
        failure {
            echo " it will throw error message when build is failed"
        }
        success {
            echo "it will display when build when build is success"
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
//plugin--> download utility plugin
//Google--> Delete directory in pipeline
 // deleteDir() -->add this in post() section in pipeline
 //plugin--> Nexus artifact uploader
 //nslookup nexus.reddy1229.onlone --> to test the DNS name is working or not
 //google --> how to call another job in jenkins pipeline with parameters
 //sol: build job
