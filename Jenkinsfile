#!/usr/bin/env groovy

node {
    stage('checkout') {
        checkout scm
    }

    stage('check java') {
        sh "java -version"
    }
    
    stage('clean') {
    withMaven(maven: 'maven-3.5') {
     sh "mvn -Pprod clean"
     }
    }
    
    stage('packaging') {
    withMaven(maven: 'maven-3.5') {
     sh "mvn -Pprod package -DskipTest"
     }
    }
    
 stage('SonarQube analysis') {
    // requires SonarQube Scanner 2.8+
    def scannerHome = tool 'sonar-runner';
    withSonarQubeEnv('My SonarQube Server') {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
    
}
