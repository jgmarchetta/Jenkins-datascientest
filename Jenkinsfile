pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                echo 'Testing schools'
                script {
                    def schools = ['Datascientest', 'DevUniversity']
                    for (int i = 0; i < schools.size(); ++i) {
                        echo "Testing the ${schools[i]} school"
                    }
                }
            }
        }
    }
}
