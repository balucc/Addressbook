#!/usr/bin/env groovy
pipeline{
        agent any
          triggers {
  pollSCM 'H/2 * * * *'
          }
 stages{
     stage('Git checkout'){
     //invoking Git repository
     step{
    git 'https://github.com/balucc/Addressbook.git'
     }}
    stage('compile'){
        //compile Java code
        step{
    withMaven(maven:'Maven'){
    sh 'mvn compile'
    }
    }}
   stage('code review'){
       //Review Java code
   try{
    withMaven(maven:'Maven'){
    sh 'mvn pmd:pmd'
   }}finally{
       stage('Publish PMD'){
           //publishing pmd report
           pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
       }
   }}
   stage('Code Testing'){
       try{
           //testing java code
       withMaven(maven:'Maven'){
       sh 'mvn test'
       }}
       finally{
           //publishing Junit test report
           junit 'target/surefire-reports/*.xml'
       }
   }
   stage('coverage check'){
       //test coverage check
       try{
       withMaven(maven:'Maven'){
       sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
       }}finally{
           //publishing cobetura report
           cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
       }
   }
   stage('packaging'){
       //packaging application
       withMaven(maven:'Maven'){
       sh 'mvn package'
   }}
 }}
