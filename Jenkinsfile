pipeline {
  agent any
  stages {
    stage('Check Out Code') {
      steps {
        git(url: 'https://github.com/lidorg-dev/NodeJS-EmptySiteTemplate.git', branch: 'master', poll: true, changelog: true)
      }
    }

    stage('Build & Compile') {
      steps {
        sh 'npm install'
      }
    }

  }
}