#!/usr/bin/env groovy

node('maven') {

    def mvnHome

    // Mark the code checkout 'stage'....
    stage('Preparation') {
        // Checkout code from repository
        checkout scm

        // Get the maven tool.
        mvnHome = tool 'M3'

        // Add MVN to the path
        env.PATH = "${mvnHome}/bin:${env.PATH}"
    }

    // Mark the code build 'stage'....
    stage('Build') {
        sh "mvn clean install"
    }

    // Mark the code deploy 'stage'....
    stage('Deploy to Nexus') {

        // Retrieve the global settings.xml
        configFileProvider([configFile(fileId: 'wb-mvn-settings', variable: 'MAVEN_SETTINGS')]) {
            sh "mvn -s $MAVEN_SETTINGS deploy"
        }
    }
}