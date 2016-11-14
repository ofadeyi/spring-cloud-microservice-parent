#!/usr/bin/env groovy

node('maven') {
    // Get the maven tool.
    def mvnHome = tool 'M3'

    // Add MVN to the path
    env.PATH = "${mvnHome}/bin:${env.PATH}"

    // Mark the code checkout 'stage'....
    stage('Checkout') {

        // Checkout code from repository
        checkout scm
    }

    // Mark the code build 'stage'....
    stage('Package and Deploy') {
        sh "mvn clean deploy"
    }
}