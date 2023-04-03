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
                    withCredentials([string(credentialsId: 'DOCKER_PWD', variable: 'DOCKER_TOKEN')]) {
                    sh 'docker build . -t aneesha9999/app30:test'
                    sh 'docker login -u aneesha9999 -p ${DOCKER_TOKEN}'
                    sh 'docker push aneesha9999/app30:test'
                    sh 'docker run -p 62:8080 -d aneesha9999/app30:test'
                }
                }
        }
            stage('Archive && clean workspace'){
                
                steps{
                    archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
                    cleanWs()

                }
            } 
    }

}