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
            steps{
              sh '''
            echo "pushing the image to dockerhub"
            docker push sivasuribabu/PYTHON-TODO-APP-PROJ:${BUILD_NUMBER}
            '''  
            }
        }
    }
}
