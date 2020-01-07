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
                playbook: 'playbook.yml',
                inventory: 'ir-nodes.yml',
                colorized: true)
        }
      }
    }
  }
}
