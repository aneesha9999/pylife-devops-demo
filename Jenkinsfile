pipeline {
    agent {
        node {
            label 'java11'
        }
    
    }

    options {
                timestamps()
                buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '2'))
                timeout(time: 240, unit: 'MINUTES')
                disableConcurrentBuilds()
                }

        stages {
            stage ('AppCodeCheckout') {
                steps {

                    git 'https://github.com/gcpcloudreddy/pylife-devops-demo.git'

                }
            }
            stage ('CI Build') {

                steps {

                    sh 'mvn clean package'
                   
                     }
    
            }

            stage ('Docker Build && Push && RUN ') {
               
                steps {
                    sh 'docker build . -t aneesha9999/app29:test'
                    sh 'docker login -u aneesha9999 -p dckr_pat_h7R41ziKv8owJCyx2j1yy1_Wzz0'
                    sh 'docker push aneesha9999/app29:test'
                    sh 'docker run -p 95:8080 -d aneesha9999/app29:test'
                }
            
        }
    }

}