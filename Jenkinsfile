#!/usr/bin/env groovy

node('maven') {

    def mvnHome
    def pom
    def version
    def branchName

    // Mark the code checkout 'stage'....
    stage('Preparation') {
        // Checkout code from repository
        checkout scm

        // Get the maven tool.
        mvnHome = tool 'M3'

        // Add MVN to the path
        env.PATH = "${mvnHome}/bin:${env.PATH}"

        // Read the branch name from git
        sh 'git rev-parse --abbrev-ref HEAD > branchName'
        branchName = readFile('branchName').trim()

        // Read the POM file and extract the versionNumber
        pom = readMavenPom file: 'pom.xml'
//        version = branchName.contains('release') ? pom.version :  pom.version.replace("-SNAPSHOT", ".${currentBuild.number}")
        version = branchName.contains('release') ? pom.version : "${pom.version}.${currentBuild.number}"

        // Set the artefact version
        sh "mvn versions:set -DnewVersion=${version}"

        println "The artefact version will be: $version"
    }

    stage('Deploy image to DockerHub') {
        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker-hub',
                          usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {

            sh "echo uname=$USERNAME pwd='${PASSWORD}'"
        }
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