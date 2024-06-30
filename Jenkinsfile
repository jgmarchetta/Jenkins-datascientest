pipeline {
    agent any
    environment { 
        DOCKER_ID = "jgmarchetta"
        DOCKER_IMAGE = "datascientestapi"
        DOCKER_TAG = "v.${BUILD_ID}.0" 
    }
    stages {
        stage('Building') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Testing') {
            steps {
                sh 'python -m unittest'
            }
        }
        stage('Deploying') {
            steps {
                script {
                    // Construire l'image Docker
                    sh "docker build -t $DOCKER_ID/$DOCKER_IMAGE:$DOCKER_TAG ."
                    
                    // Déployer l'image Docker
                    sh "docker run -d -p 8000:8000 --name datascientest $DOCKER_ID/$DOCKER_IMAGE:$DOCKER_TAG"
                }
            }
        }
    }
}
