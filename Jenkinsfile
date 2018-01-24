pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            powershell(script: './TestinJen/PShell/APP_Int.ps1', returnStatus: true, returnStdout: true)
          }
        }
        stage('Harden OS') {
          steps {
            powershell(script: './TestingJen/PShell/Import-GPO.ps1', returnStatus: true, returnStdout: true)
            powershell(script: './TestinJen/PShell/Get-GPOReport.ps1', returnStatus: true, returnStdout: true)
          }
        }
        stage('Build App') {
          agent any
          steps {
            powershell(script: './TestinJen/PS/App.ps1', returnStatus: true, returnStdout: true)
            input(message: 'App Script Completed?', id: 'Yes', ok: 'No')
          }
        }
      }
    }
    stage('Tools added') {
      agent any
      steps {
        bat(script: './Agents.msi', returnStatus: true, returnStdout: true)
        waitUntil() {
          validateDeclarativePipeline '//Agents'
        }
        
        echo 'Agent [XXXXX] found'
        powershell(script: '/TestJen/PShell/Agent.ps1', returnStatus: true, returnStdout: true)
        echo 'Agent Updated'
        timeout(time: 5) {
          echo 'Rdy for next agent'
        }
        
        powershell(script: './TestinJen/PShell/MAgent.ps1', returnStatus: true, returnStdout: true)
        waitUntil() {
          fileExists '/M/Agent'
        }
        
        echo 'MAgent found'
      }
    }
    stage('TEST') {
      parallel {
        stage('TEST') {
          environment {
            CI = 'True'
          }
          steps {
            sh 'Test'
          }
        }
        stage('Burning') {
          steps {
            sh 'Test'
          }
        }
        stage('Cooling') {
          steps {
            sh 'Test'
          }
        }
      }
    }
    stage('Wrapping ') {
      steps {
        sh 'Test'
      }
    }
    stage('Deploy') {
      steps {
        sh 'Test'
      }
    }
  }
}