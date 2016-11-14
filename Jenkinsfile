#!/usr/bin/env groovy

node('maven') {

    def mvnHome
    // Mark the code checkout 'stage'....
    stage('Preparation') {
        // Checkout code from repository
        checkout scm

        // Get the maven tool.
        mvnHome = tool 'M3'

    }

    // Mark the code build 'stage'....
    stage('Package and Deploy') {
        // Add MVN to the path
        env.PATH = "${mvnHome}/bin:${env.PATH}"

        // Retrieve the global settings.xml
        configFileProvider([configFile(fileId: 'wb-mvn-settings', variable: 'MAVEN_SETTINGS')]) {
            sh "mvn -s $MAVEN_SETTINGS clean deploy"
        }
    }
}