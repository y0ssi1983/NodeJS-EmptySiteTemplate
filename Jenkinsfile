pipeline {
  agent any
  stages {
    stage('checkout-code') {
      parallel {
        stage('checkout-code') {
          steps {
            git(url: 'git@github.com:y0ssi1983/NodeJS-EmptySiteTemplate.git', branch: 'master', credentialsId: 'github')
          }
        }

        stage('say hello') {
          steps {
            sh '''echo "hello"
'''
          }
        }

      }
    }

    stage('build') {
      steps {
        sh 'npm install'
      }
    }

  }
}