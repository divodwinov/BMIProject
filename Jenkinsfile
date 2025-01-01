pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'divodwinov/BMIProject:latest'
        CONTAINER_NAME = 'BMICalculator'
        PORT_MAPPING = '8081:80' // Adjust the port mapping as needed
    }

    stages {

        stage('Clean Up Existing Containers') {
            steps {
                script {
                    // Stop and remove any existing container with the same name
                    bat """
                    docker ps -q -f name=${CONTAINER_NAME} | for /F "delims=" %%i in ('more') do docker stop %%i
                    docker ps -aq -f name=${CONTAINER_NAME} | for /F "delims=" %%i in ('more') do docker rm %%i
                    """
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    bat "docker build -t ${DOCKER_IMAGE} -f Dockerfile ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container
                    bat "docker run -d -p ${PORT_MAPPING} --name ${CONTAINER_NAME} ${DOCKER_IMAGE}"
                }
            }
        }

        stage('Verify Container') {
            steps {
                script {
                    // Verify that the container is running
                    bat "docker ps -f name=${CONTAINER_NAME}"
                }
            }
        }

        stage('Health Check') {
            steps {
                script {
                    // Check if the application is responding (replace with a curl command if needed)
                    bat """
                    timeout 5
                    curl -I http://localhost:${PORT_MAPPING.split(':')[0]} || echo Health check failed!
                    """
                }
            }
        }
    }
}
