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
           //publishing pmd report
           success {
              stage('Publish PMD'){
           pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
          }}}
       }
   }}

