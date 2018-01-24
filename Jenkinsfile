pipeline {
  agent any
  stages {
    stage('Find') {
      steps {
        node(label: 'WrkSt')
      }
    }
  }
  environment {
    Stageing = '01'
  }
}