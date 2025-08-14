pipeline {
    agent any

    environment {
        IMAGE_NAME      = "jenkins-flask-demo"
        DOCKER_REGISTRY = "ajithsunkara96"
        IMAGE_TAG       = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/ajithsunkara96/jenkins-flask-cicd.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                  set -e
                  command -v pip3 >/dev/null 2>&1 || { sudo apt-get update && sudo apt-get install -y python3-pip; }
                  pip3 install --upgrade pip
                  pip3 install -r flask-app/requirements.txt
                '''
            }
        }

        stage('Unit Test') {
            steps {
                sh 'pytest -q flask-app/test_app.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                  set -e
                  docker build -t $IMAGE_NAME ./flask-app
                  docker tag $IMAGE_NAME $DOCKER_REGISTRY/$IMAGE_NAME:$IMAGE_TAG
                  docker tag $IMAGE_NAME $DOCKER_REGISTRY/$IMAGE_NAME:latest
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
                    sh '''
                      set -e
                      echo "$DOCKER_TOKEN" | docker login -u "$DOCKER_REGISTRY" --password-stdin
                      docker push $DOCKER_REGISTRY/$IMAGE_NAME:$IMAGE_TAG
                      docker push $DOCKER_REGISTRY/$IMAGE_NAME:latest
                    '''
                }
            }
        }

        stage('Deploy via Docker Compose') {
            steps {
                sh '''
                  set -e
                  docker-compose down || true
                  docker-compose up -d --build
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Image: $DOCKER_REGISTRY/$IMAGE_NAME:$IMAGE_TAG"
        }
        failure {
            echo '❌ Build failed.'
        }
    }
}
