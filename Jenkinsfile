pipeline{
	agent any
	stages{
	 stage('Git checkout'){
	 steps{
	 git 'https://github.com/balucc/Addressbook.git'
	}}
	 steps{
           withMaven(maven:'Maven'){
             sh 'mvn compile'
	  }}
	stage('Code Review'){
	  try{
           steps{
            withMaven(maven:'Maven'){
             sh 'mvn pmd:pmd'
             }}
             }
      }
      finally{
       stage('Publish PMD'){
       pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
       }
	}
   }
}
