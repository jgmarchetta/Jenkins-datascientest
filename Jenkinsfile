pipeline {
    agent any
    environment { 
        DOCKER_ID = "dstdockerhub"
        DOCKER_IMAGE = "datascientestapi"
        DOCKER_TAG = "v.${BUILD_ID}.0"
    }
    stages {
        stage('Building') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }
        stage('Testing') {
            steps {
                sh 'python3 -m unittest discover -s tests'
            }
        }
        stage('Building Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_ID}/${DOCKER_IMAGE}:${DOCKER_TAG} ."
            }
        }
        stage('Pushing Docker Image') {
            steps {
                sh "docker push ${DOCKER_ID}/${DOCKER_IMAGE}:${DOCKER_TAG}"
            }
        }
        stage('Deploying') {
            steps {
                echo 'Deploying application...'
                // Ajoutez vos commandes de déploiement ici
            }
        }
    }
}
