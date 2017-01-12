#!/usr/bin/env groovy

node('maven') {

    def mvnHome
    def pom
    def version
    def branchName
    def releaseBranch = "master"

    // Mark the code checkout 'stage'....
    stage('Preparation') {
        // Checkout code from repository
        checkout scm

        // Get the maven tool.
        mvnHome = tool 'M3'

        // Add MVN to the path
        env.PATH = "${mvnHome}/bin:${env.PATH}"

        // Read the branch name from git
        sh 'git branch -a --contains $(git rev-parse --short HEAD) --merged > branchName'
        branchName = readFile('branchName').trim()
        println "Releasing from branch: $branchName"

        // Read the POM file and extract the versionNumber
        pom = readMavenPom file: 'pom.xml'
        version = branchName.contains(releaseBranch) ? pom.version : "${pom.version}.${currentBuild.number}"

        // Set the artefact version
        println "The artefact version will be: $version"
        sh "mvn versions:set -DnewVersion=${version}"
    }

    // Mark the code build 'stage'....
    stage('Build') {
        // Retrieve the global settings.xml
        configFileProvider([configFile(fileId: 'wb-mvn-settings', variable: 'MAVEN_SETTINGS')]) {
            sh "mvn -s $MAVEN_SETTINGS clean install"
        }
    }

    // Mark the code deploy 'stage'....
    stage('Deploy to Nexus') {
        // Retrieve the global settings.xml
        configFileProvider([configFile(fileId: 'wb-mvn-settings', variable: 'MAVEN_SETTINGS')]) {
            // Deploy to artefacts repository
            sh "mvn -s $MAVEN_SETTINGS -Dmaven.test.skip=true deploy"
        }
    }


}
