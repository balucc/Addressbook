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
            pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
          }} 
       }
   }
 }
stage('Code Testing'){
    steps{
        script{
           try{
             withMaven(maven:'Maven'){
              sh 'mvn test'
             }
           }
       finally{
           junit 'target/surefire-reports/*.xml'
      }
    }
   }
  }
stage('coverage check'){
    steps{
      script{
        try{
          withMaven(maven:'Maven'){
             sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
          }
         }
       finally{
           cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
       }
      }
     }
   }
stage('packaging'){
   steps{
       withMaven(maven:'Maven'){
       sh 'mvn package'
    }
   }
  }
stage('Docker Image Build'){
  steps{
    script{
     sh cp /var/lib/jenkins/workspace/javaPackage/target/addressbook.war .
        sudo docker build . -t balucc/addressbook:$BUILD_NUMBER
        sudo docker push balucc/addressbook:$BUILD_NUMBER
    }
  }
 }
 }
}


