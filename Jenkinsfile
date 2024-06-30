pipeline {
    agent any

    environment { 
        DOCKER_ID = "jgmarchetta"
        DOCKER_IMAGE = "datascientestapi"
        DOCKER_TAG = "v.${BUILD_ID}.0" 
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Building') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Testing') {
            steps {
                script {
                    sh 'python3 -m unittest'
                }
            }
        }

        stage('Deploying') {
            steps {
                script {
                    // Supprimer le conteneur s'il existe
                    sh 'docker ps -a | grep jenkins && docker rm -f jenkins || true'
                    
                    // Construire l'image Docker
                    sh 'docker build -t $DOCKER_ID/$DOCKER_IMAGE:$DOCKER_TAG .'
                    
                    // Exécuter le conteneur Docker en liant un autre port si 8000 est occupé
                    sh 'docker run -d -p 8000:8000 --name jenkins $DOCKER_ID/$DOCKER_IMAGE:$DOCKER_TAG'
                }
            }
        }

        stage('User Acceptance') {
            steps {
                input(
                    message: "Proceed to push to main",
                    ok: "Yes"
                )
            }
        }

        stage('Pushing and Merging') {
            parallel {
                stage('Pushing Image') {
                    steps {
                        script {
                            try {
                                withCredentials([usernamePassword(credentialsId: 'docker_jenkins', passwordVariable: 'DOCKERHUB_CREDENTIALS_PSW', usernameVariable: 'DOCKERHUB_CREDENTIALS_USR')]) {
                                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                                    sh 'docker push $DOCKER_ID/$DOCKER_IMAGE:$DOCKER_TAG'
                                }
                            } catch (Exception e) {
                                echo "Failed to push image: ${e.message}"
                                currentBuild.result = 'FAILURE'
                                error 'Pushing image failed'
                            }
                        }
                    }
                }
                stage('Merging') {
                    steps {
                        echo 'Merging done'
                        // Ajoutez vos étapes de fusion ici si nécessaire
                    }
                }
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
