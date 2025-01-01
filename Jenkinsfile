pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'divodwinov/BMIProject:latest'
        CONTAINER_NAME = 'BMICalculator'
        PORT_MAPPING = '8081:80' // Adjust the port mapping as needed
    }

    stages {

      

        stage('Build Docker Image') {
            steps {
                script {
                    bat "docker build -t ${DOCKER_IMAGE} -f Dockerfile ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    bat "docker run -d -p ${PORT_MAPPING} --name ${CONTAINER_NAME} ${DOCKER_IMAGE}"
                }
            }
        }

      
    }
}
