pipeline{
    agent any
    stages{
        stage('git checkout'){
            steps{
                git credentialsId: 'GitAccountCred', url: 'https://github.com/balucc/Addressbook.git'
            }
        }
        stage('compile') {
            steps {
                 sh 'mvn compile'
                }

            tools {
                  maven 'Maven3.9'
                }
        }
                      
            }
        }
    
