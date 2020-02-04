pipeline {
  agent {
    label 'control'
  }
  
  environment {  
      ANSIBLE_CREDS = credentials('ansible-deployment-pwd-id')
  }

  stages {
    stage('checkout') {
      steps {
        checkout scm
      }
    } 
    stage('Security check'){
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
    
    stage('Run ansible'){
        when {
            expression {
                !skipRemainingStages
            }
        }
      steps{
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
