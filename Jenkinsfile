pipeline {
  agent any
  
  tools {
//     supports only maven, gradle, jdk
    gradle 'Gradle 8.0-milestone-2'
  }
  
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
//         withGradle() {
//           sh './gradlew -v'
//         }
        
//         can run without wrapper since gradle is defined here
        sh './gradlew -v'
      }
    }
  }
}
