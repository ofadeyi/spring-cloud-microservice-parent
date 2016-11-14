#!/usr/bin/env groovy

node('maven') {
    // Mark the code checkout 'stage'....
    stage 'Checkout'

    // Checkout code from repository
    checkout scm

    // Get the maven tool.
    def mvnHome = tool 'M3'

    // Add MVN to the path
    env.PATH = "${mvnHome}/bin:${env.PATH}"

    configFileProvider([configFile(fileId: 'maven-settings', variable: 'MAVEN_SETTINGS')]) {
        // Mark the code build 'stage'....
        stage 'Package and Deploy'
        sh "mvn -s $MAVEN_SETTINGS clean deploy"
    }
}