#!/usr/bin/env groovy

node {
    stage('checkout') {
        checkout scm
    }

    docker.image('openjdk:8').inside('-u root') {
        stage('check java') {
            sh "java -version"
        }

        stage('quality analysis') {
            withSonarQubeEnv('sonar-server') {
            }
        }
    }

    def dockerImage
    stage('build docker') {
    }

    stage('publish docker') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-login') {
            dockerImage.push 'latest'
        }
    }
}
