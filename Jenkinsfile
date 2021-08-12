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
curl localhost:8080
if [[ "x$?" == "x0" ]]; 
then    echo good; 
else exit 1; 
fi'''
      }
    }

    stage('Package Code') {
      parallel {
        stage('Package Code') {
          steps {
            sh 'tar -czvf node.tar.gz * '
          }
        }

        stage('notify slack') {
          steps {
            slackSend(channel: 'devops_december2020', color: '#3EA652', message: 'job success')
          }
        }

      }
    }

    stage('Publish the Archive') {
      steps {
        archiveArtifacts 'node.tar.gz'
        cleanWs(cleanWhenAborted: true, cleanWhenFailure: true, cleanWhenNotBuilt: true, cleanWhenSuccess: true, cleanWhenUnstable: true)
      }
    }

  }
}
