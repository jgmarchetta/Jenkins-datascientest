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
                sh '/chemin/vers/votre/python/bin/python -m pip install -r requirements.txt'
            }
        }
        stage('Testing') {
            steps {
                sh '/chemin/vers/votre/python/bin/python -m unittest'
            }
        }
        stage('Deploying') {
            steps {
                script {
                    // Exemple : Docker build et run
                    sh "docker build -t $DOCKER_ID/$DOCKER_IMAGE:$DOCKER_TAG ."
                    sh "docker run -d -p 8000:8000 --name datascientest $DOCKER_ID/$DOCKER_IMAGE:$DOCKER_TAG"
                }
            }
        }
    }
}

