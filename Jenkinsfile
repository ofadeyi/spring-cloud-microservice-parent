#!/usr/bin/env groovy

// Mark the code checkout 'stage'....
stage 'Checkout'
node('maven') {
    // Checkout code from repository
    checkout scm
}

// Mark the code build 'stage'....
stage 'Package and Deploy'
node('maven') {
    // Get the maven tool.
    def mvnHome = tool 'M3'

    // Add MVN to the path
    env.PATH = "${mvnHome}/bin:${env.PATH}"

    configFileProvider([configFile(fileId: '008de1b0-03e4-4265-a6f6-78d8806b4103', variable: 'MAVEN_SETTINGS')]) {
        sh "mvn -s $MAVEN_SETTINGS clean deploy"
    }
}
