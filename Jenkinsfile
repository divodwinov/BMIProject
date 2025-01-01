pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'divodwinov/bmiproject:latest'
        CONTAINER_NAME = 'bmicalculator'
        PORT_MAPPING = '8081:80'
        DOCKER_PATH = 'C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe'
    }

    stages {
        stage('Clean Up Existing Containers') {
            steps {
                script {
                    bat """
                    if ${DOCKER_PATH} ps -q -f name=${CONTAINER_NAME} >nul 2>&1 (
                        ${DOCKER_PATH} stop ${CONTAINER_NAME}
                        ${DOCKER_PATH} rm ${CONTAINER_NAME}
                    )
                    """
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat "${DOCKER_PATH} build -t ${DOCKER_IMAGE} -f Dockerfile ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    bat "${DOCKER_PATH} run -d -p ${PORT_MAPPING} --name ${CONTAINER_NAME} ${DOCKER_IMAGE}"
                }
            }
        }
    }
}
