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
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker-cred', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')])
            sh '''
            echo "pushing the image to dockerhub"
            docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
            docker push sivasuribabu/todo-app:${BUILD_NUMBER}
            '''  
            }
        }
    }
}
