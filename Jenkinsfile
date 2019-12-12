pipeline{
	agent any
	stages{
	 stage('Git checkout'){
	 steps{
	 git 'https://github.com/balucc/Addressbook.git'
	  }
	}
 stage('compile'){
	 steps{
           withMaven(maven:'Maven'){
             sh 'mvn compile'
	    }
	  }
	}
	stage('Code Review'){
steps{
	script{
	   try{
            withMaven(maven:'Maven'){
             sh 'mvn pmd:pmd'
             }
           }
      finally{
         stage('Publish PMD'){
         steps{
            pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
          }} 
       }
	 }
   }
 }
}
}
