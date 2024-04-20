pipeline {
    
    agent any 
    
    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
    }
    stages {
        stage('Checkout'){
           steps {
           	sh 'echo passed'
           }
        }
        stage('biuld docker image'){
            steps{ 
                 sh 'docker build -t todo-app .'
            }  
        }
        stage('SAST'){
              environment {
                  SONAR_URL = "http://192.168.225.162:9000"
              }
              steps{
                  withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_AUTH_TOKEN')]) {
                      sh 'sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
                  }
                  
              }
       }
        
      
    }
}
