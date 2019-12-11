#!/usr/bin/env groovy
pipeline{
 agent any
   stages{
       stage('Git checkout'){
        //invoking Git repository
         steps{
           git 'https://github.com/balucc/Addressbook.git'
         }}
        stage('compile'){
         //compile Java code
        steps{
           withMaven(maven:'Maven'){
             sh 'mvn compile'
           }
          }
        }
       stage('code review'){
        //Review Java code
          try{
           steps{
            withMaven(maven:'Maven'){
             sh 'mvn pmd:pmd'
             }}
             }
          finally{
         stage('Publish PMD'){
           //publishing pmd report
          steps{
           pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
          }}
       }
   }
   stage('Code Testing'){
       try{
           //testing java code
           steps{
       withMaven(maven:'Maven'){
       sh 'mvn test'
       }
       }}
       finally{
           //publishing Junit test report
           steps{
           junit 'target/surefire-reports/*.xml'
       }}
   }
   stage('coverage check'){
       //test coverage check
       try{
       steps{
       withMaven(maven:'Maven'){
       sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
       }
       }}
       finally{
           //publishing cobetura report
           steps{
           cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
       }}
   }
   stage('packaging'){
       steps{
       //packaging application
       withMaven(maven:'Maven'){
       sh 'mvn package'
   }}
 }
    stage('docker-image-build'){
      //build docker image with addressbook.war file
     steps{
       sh 'cp /var/lib/jenkins/workspace/javaPackage/target/addressbook.war .'
       sh 'sudo docker build . -t balucc/addressbook:BUILD_NUMBER'
       sh 'sudo docker push balucc/addressbook:$BUILD_NUMBER'
      }}
}}
