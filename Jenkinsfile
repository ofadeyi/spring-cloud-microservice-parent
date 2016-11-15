#!/usr/bin/env groovy

node('maven') {

    def mvnHome
    def mvnSettings

    // Mark the code checkout 'stage'....
    stage('Preparation') {
        // Checkout code from repository
        checkout scm

        // Get the maven tool.
        mvnHome = tool 'M3'

        // Add MVN to the path
        env.PATH = "${mvnHome}/bin:${env.PATH}"

        configFileProvider([configFile(fileId: 'wb-mvn-settings', variable: 'MAVEN_SETTINGS')]) {
            mvnSettings = MAVEN_SETTINGS
        }
    }

    // Mark the code build 'stage'....
    stage('Build') {
        sh "mvn -s $mvnSettings clean install"
    }

//    // Mark the code deploy 'stage'....
//    stage('Deploy to Nexus') {
//
//        // Retrieve the global settings.xml
//        configFileProvider([configFile(fileId: 'wb-mvn-settings', variable: 'MAVEN_SETTINGS')]) {
//            sh "mvn -s $MAVEN_SETTINGS deploy"
//        }
//    }
}