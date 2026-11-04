
pipeline {
    agent any

    environment {
        IMAGE_NAME = 'python-crud-api'
        CONTAINER_NAME = 'production-api-container'
        VOLUME_NAME = 'production-api-data'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Syntax Check') {
            steps {
                sh 'python3 -m py_compile app.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -d \
                        --name ${CONTAINER_NAME} \
                        -p 5000:5000 \
                        -v ${VOLUME_NAME}:/var/lib/backend_data \
                        ${IMAGE_NAME}:${BUILD_NUMBER}
                '''
            }
        }

        stage('Health Check') {
            steps {
                sleep(time: 5, unit: 'SECONDS')
                sh 'curl -f http://host.docker.internal:5000/health'
            }
        }
    }
}
