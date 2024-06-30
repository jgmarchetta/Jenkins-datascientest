pipeline {
    agent any
  // au niveau de la pipeline
    environment {
        OUTPUT_PATH = './outputs/'
    }
    stages {
        stage ('build') {
      // au niveau d'un stage
      environment {
            OUTPUT_PATH = './outputs/'
        }
            ...
        }
    ...
    }
}
