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
        stage('pushing docker image'){
            sh '''
            echo "pushing the image to dockerhub"
            dicker push sivasuribabu/PYTHON-TODO-APP-PROJ:${BUILD_NUMBER}
            '''
        }
    }
}
