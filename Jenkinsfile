#!/usr/bin/env groovy

node('maven') {
    // Mark the code checkout 'stage'....
    stage 'Checkout'

    // Checkout code from repository
    checkout scm

    // Get the maven tool.
    def mvnHome = tool 'M3'

    // Mark the code build 'stage'....
    stage 'Package and Deploy'
    sh "${mvnHome}/bin/mvn clean deploy"
}