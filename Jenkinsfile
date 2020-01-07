pipeline {
  agent {
    label 'control'
  }

  stages {
    stage('checkout') {
      steps {
        checkout scm
      }
    } 
    stage('update java'){
      steps {
        sh 'ls -ah'
      }
    }
  }
}
