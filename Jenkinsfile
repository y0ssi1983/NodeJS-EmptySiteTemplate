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
      steps {
        sh 'node server.js'
      }
    }

  }
}