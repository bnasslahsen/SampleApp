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
    
 stage('SonarQube analysis') {
    // requires SonarQube Scanner 2.8+
    def scannerHome = tool 'SonarQube Scanner 2.8';
    withSonarQubeEnv('My SonarQube Server') {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
    
}
