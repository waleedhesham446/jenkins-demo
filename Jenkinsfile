CODE_CHANGES = getGitChanges()
pipeline {

  agent any
  
  environment {
    NEW_VERSION = '1.3.0'
    SERVER_CREDENTIALS = credentials('system')  //  credentials ID
  }
  
  tools {
    
  }
  
  parameters {
    string(name: 'VERSION', defaultValue: '', description: 'version to deploy on prod')
    choice(name: '_VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
    booleanParam(name: 'executeDeploy', defaultValue: true, description: '')
  }
  
  stages {
    
    stage("build") {
      when {
        expression {
          BRANCH_NAME == 'dev' && CODE_CHANGES == true
        }
      }
      steps {
        echo 'building the application'
        echo "building version ${NEW_VERSION}"
      }
    }
    
    stage("test") {
      when {
        expression {
          BRANCH_NAME == 'dev' || BRANCH_NAME == 'master'
        }
      }
      
      steps {
        echo 'testing the application'
      }
    }
    
    stage("deploy") {
      when {
        expression {
          //   params.executeDeploy
          params.executeDeploy == true
        }
      }
      steps {
        echo "deploying the application version ${params.VERSION}"
        echo "deploying with ${SERVER_CREDENTIALS}"
        sh "${SERVER_CREDENTIALS}"
        
        //  another way to access credentials
        withCredentials([
          usernamePassword(credentials: 'system', usernameVariable: USER, passwordVariable: PWD)
        ]) {
          sh "echo ${USER}:${PWD}"
        }
      }
    }
  }
  
  post {
    always {
      sh 'echo finished'
    }
    
    success {
      sh 'echo succeeded'
    }
    
    failure {
      sh 'echo failed'
    }
  }
}
