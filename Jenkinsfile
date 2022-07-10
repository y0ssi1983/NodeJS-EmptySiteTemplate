pipeline {
  agent {
    node {
      label 'docker-centos-7'
    }

  }
  stages {
    stage('checkout-code') {
      parallel {
        stage('checkout-code') {
          steps {
            git(url: 'git@github.com:y0ssi1983/NodeJS-EmptySiteTemplate.git', branch: 'master', credentialsId: 'github')
          }
        }

        stage('say hello to me') {
          steps {
            sh 'echo "Hello"'
          }
        }

      }
    }

    stage('build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test App') {
      parallel {
        stage('Run the App') {
          steps {
            sh 'node server.js'
          }
        }

        stage('check if app is running') {
          steps {
            sh '''sleep 5
curl localhost:8081
if [[ $(echo #?) == 0 ]]
then
  echo "success"
  ps -ef | grep node | awk \'{print$2}\' | kill
  exit 0
else
  echo "failure"
  exit 1
fi'''
          }
        }

      }
    }

  }
}