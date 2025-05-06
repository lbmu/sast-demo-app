pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        checkout([$class: 'GitSCM',
        branches: [[name: 'main']],
        userRemoteConfigs: [[url: 'https://github.com/lbmu/sast-demo-app']]
        ])
        }
      }
    stage('Install Dependencies') {
      steps {
        sh 'pip install bandit'
        }
      }
    stage('SAST Analysis') {
      steps {
        sh 'bandit -f xml -o bandit-output.xml -r . || true'
        recordIssues tools: [bandit(pattern: 'bandit-output.xml')]
        }
      }
    }
  }
