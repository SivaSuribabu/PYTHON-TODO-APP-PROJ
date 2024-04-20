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
                 sh '''
                 echo " Building docker image"
                 docker build -t sivasuribabu/todo-app:${BUILD_NUMBER} .
                 '''
            }  
        }
        stage('pushing docker image'){
            environment{
                REGISTRY_CREDENTIALS = credentials('docker-cred')
            }
            steps{
            sh '''
            echo "pushing the image to dockerhub"
            docker push sivasuribabu/todo-app:${BUILD_NUMBER}
            '''  
            }
        }
    }
}
