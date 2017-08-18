#!/usr/bin/env groovy

node {
    stage('checkout') {
        checkout scm
    }

    stage('check java') {
        sh "java -version"
    }

    stage('clean') {
        sh "./mvnw clean"
    }
    
    stage('backend tests') {
        sh "./mvnw test"
    }
    
     stage('packaging') {
        sh "./mvnw package -Pprod -DskipTests"
    }
    
    stage('quality analysis') {
        withSonarQubeEnv('Sonar') {
        }
    }
}
