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
            sh ' docker build -t todo-app .'
        }
        
      
    }
}
