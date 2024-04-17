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

        stage('Build Docker'){
            steps{
                script{
                    sh '''
                    echo 'Buid Docker Image'
                    docker build -t sivasuribabu/todo-app:${BUILD_NUMBER} .
                    '''
                }
            }
        }
        
        
      	stage("static code analysis"){
      		environment {
      			SONAR_URL = "http://192.168.225.162:9000/"
      		}
      	
      		steps{
      			withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_AUTH_TOKEN')]) {
      			  mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}
      			}
      		}
      	}
      

        stage('Build and Push Docker Image') {
        	environment{
        		DOCKER_IMAGE = "sivasuribabu/todo-app:${BUILD_NUMBER}"
        		REGISTRY_CREDENTIALS = credentials('docker-cred')
        	}
        	
        	  steps {
        		script {
            			def dockerImage = docker.image("${DOCKER_IMAGE}")
            			docker.withRegistry('https://index.docker.io/v1/', "docker-cred") {
                			dockerImage.push()
            			}
        		}
      		}
        }
        
         stage('Update Deployment File') {
           environment {
            GIT_REPO_NAME = "PYTHON-TODO-APP-PROJ"
            GIT_USER_NAME = "SivaSuribabu"
          }
        	steps {
            	 withCredentials([string(credentialsId: 'github', variable: 'GITHUB_TOKEN')]) {
                	sh '''
                	    git config user.email "siva.xyz@gmail.com"
                    	git config user.name "Siva Suribabu"
                    	BUILD_NUMBER=${BUILD_NUMBER}
                    	sed -i "s/replaceImageTag/${BUILD_NUMBER}/g" todo-app-manifests/todoapp-deployment.yml
                    	git add main/todo-app-manifests/todoapp-deployment.yml
                    	git commit -m "Update deployment image to version ${BUILD_NUMBER}"
                    	git push https://${GITHUB_TOKEN}@github.com/${GIT_USER_NAME}/${GIT_REPO_NAME} HEAD:main
                	'''
             	}
          }
      }
      
      
    }
}
