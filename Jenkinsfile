pipeline {
  agent any
  stages {
    stage("Run frontend") {
      steps {
        echo 'executing yarn...'
        nodejs('Node-10.17') {
          sh 'yarn install'
        }
      }
    }
    stage("Run backend") {
      steps {
        echo 'executing gradle...'
        withGradle() {
          sh './gradlew -v'
        }
      }
    }
  }
}
