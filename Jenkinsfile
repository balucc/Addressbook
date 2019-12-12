pipeline{
	agent any
	stages{
	 stage('Git checkout'){
	 steps{
	 git 'https://github.com/balucc/Addressbook.git'
	}}
	stage('compile'){
	  steps{
	   tool {
	     maven 'Maven'
	  }
	   steps{
	    sh 'mvn compile'
	  }}
	}
     }
   }
