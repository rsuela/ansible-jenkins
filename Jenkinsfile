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
        script {
          def userInput = input(id: 'userInput', message: 'Password for deployment?', parameters: [password(defaultValue: '', description: '', name: '')])
          if ("${userInput}" == "$ANSIBLE_CREDS"){
              echo "proceed with deployment"
              skipRemainingStages = false
          } else {
              echo "Incorrect password. Aborting deployment."
              skipRemainingStages = true
              currentBuild.result = 'FAILURE'
              return
          }
        }
      }
    }
    
    stage('run ansible'){
        when {
            expression {
                !skipRemainingStages
            }
        }
        ansiColor('xterm') {
            ansiblePlaybook(
                playbook: 'rolling_update.yml',
                inventory: 'ir-inventory.yml',
                colorized: true)
        } 
    }
  }
}
