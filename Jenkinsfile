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
        ansiColor('xterm') {
            ansiblePlaybook(
                playbook: 'rolling_update.yml',
                inventory: 'ir-inventory.yml',
                colorized: true)
        }
      }
    }
  }
}
