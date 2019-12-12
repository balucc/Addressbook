<<<<<<< HEAD
pipeline{
 agent any
 stages{
stage('code review'){
        //Review Java code
           steps{
            withMaven(maven:'Maven'){
             sh 'mvn pmd:pmd'
             }}
        post{
=======
#!/usr/bin/env groovy
node{
    stage('Git checkout'){
        //invoking Git repository
    git 'https://github.com/balucc/Addressbook.git'
    }
    stage('compile'){
        //compile Java code
    withMaven(maven:'Maven'){
    sh 'mvn compile'
    }}
   stage('code review'){
       //Review Java code
   try{
    withMaven(maven:'Maven'){
    sh 'mvn pmd:pmd'
   }}finally{
       stage('Publish PMD'){
>>>>>>> parent of 18fdc88... Update Jenkinsfile
           //publishing pmd report
           success {
              stage('Publish PMD'){
           pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
          }}}
       }
   }}

