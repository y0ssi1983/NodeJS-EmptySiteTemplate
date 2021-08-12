pipeline {
  agent {
    node {
      label 'centos7-nodejs'
    }

  }
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

    stage('Test Code') {
      steps {
        sh '''node server.js &
sleep 5 &&
curl localhost:8082
if [[ "x$?" == "x0" ]]; 
then    echo good; 
else exit 1; 
fi'''
      }
    }

  }
}