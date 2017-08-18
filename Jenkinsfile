#!/usr/bin/env groovy

node {
    stage('checkout') {
        checkout scm
    }

    stage('check java') {
        sh "java -version"
    }
    
    stage('backend tests') {
        withMaven('mvn -Prod test')
    }
    
     stage('packaging') {
       withMaven('mvn -Prod package -Pprod -DskipTests')
    }
    
 stage('SonarQube analysis') {
    // requires SonarQube Scanner 2.8+
    def scannerHome = tool 'SonarQube Scanner 2.8';
    withSonarQubeEnv('My SonarQube Server') {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
    
}
