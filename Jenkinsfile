// at the pipeline and stage level
pipeline {
    agent any
    environment {
         nom = 'datascientest'
    }
    stages {
        stage('Example') {
            environment {
                AN_ACCESS_KEY = credentials('datascientest-secret')  // variable secret
            }
            steps {
                sh 'print $nom' // variable call
            }
        }
    }
}
