pipeline {
    agent any
    environment {
        APP_NAME = "test app name"
    } 
    stages {
        stage('Build Image' ) {
            steps {
        sh "echo ${env.APP_NAME}"
            }
        }
        stage("Build Stahe (Docker)"){
            agent { label "build-server" }
            steps {
                sh "docker build -t ghcr.io/apisitssi/sdfnhsfnhfs ."
            }
        }
        stage('Deliver Docker Image') {
            agent {label 'build-server'}
            steps {
                withCredentials(
                [usernamePassword(
                    credentialsId: 'apisitssi',
                    passwordVariable: 'githubPassword',
                    usernameVariable: 'githubUser'
                )]
            ){
                sh "docker login ghcr.io -u ${env.githubUser} -p ${env.githubPassword}"
                sh "docker push ${env.IMAGE_NAME}:${env.BUILD_NUMBER}"
            }
            }
        }
    }
}        