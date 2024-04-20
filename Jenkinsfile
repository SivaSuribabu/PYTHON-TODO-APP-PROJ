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
                withCredentials([usernamePassword(credentialsId: 'docker-cred', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                }
            sh '''
            echo "pushing the image to dockerhub"
            docker push sivasuribabu/todo-app:${BUILD_NUMBER}
            '''  
            }
        }

      stage('updating deployment file'){
            environment {
                GIT_REPO_NAME = "PYTHON-TODO-APP-PROJ"
                GIT_USER_NAME = "SivaSuribabu"
            }
            steps{
                withCredentials([string(credentialsId: 'github', variable: 'GITHUB_TOKEN')]) {
                    sh '''
                    git config user.email "sivasuribabupenkey@gmail.com"
                    git config user.name "Siva Suribabu"
                    BUILD_NUMBER=${BUILD_NUMBER}
                    sed -i "s/replaceImageTag/${BUILD_NUMBER}/g" deploy/deploy.yml
                    git add deploy/deploy.yml
                    git commit -m "Update deployment image to version ${BUILD_NUMBER}"
                    git push https://${GITHUB_TOKEN}@github.com/${GIT_USER_NAME}/${GIT_REPO_NAME} HEAD:main
                    '''
            }
      }
    }
 }
}
