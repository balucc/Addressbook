pipeline{
	agent any
	stages{
	 stage('Git checkout'){
	 steps{
	 git 'https://github.com/balucc/Addressbook.git'
	}}
	stage('compile'){
	   tool{
	     maven 'Maven'
	  }
	   steps{
	    sh 'mvn compile'
	  }}
	stage('Code Review'){
	tool{
	   maven 'Maven'
	   }
	    try{
	 sh 'mvn pmd:pmd'
      }
      finally{
       stage('Publish PMD'){
       pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
       }
	}
   }
}
}
