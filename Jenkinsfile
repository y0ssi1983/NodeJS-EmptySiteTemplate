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
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
              sh 'node server.js'
            }

          }
        }

        stage('check if app is running') {
          steps {
            sh '''sleep 5
curl localhost:8081
if [ $(echo $?) -eq 0 ];
then
  echo "success"
  ps -ef | grep node | awk \'{print$2}\' | head -n 1 | xargs kill
  exit 0
else
  echo "failure"
  exit 1
fi'''
          }
        }

      }
    }

    stage('Package') {
      steps {
        sh '''mkdir target && rsync -Rr . target/
tar -czvf package-$BUILD_ID.tar.gz target/
'''
      }
    }

    stage('archive artifact') {
      steps {
        archiveArtifacts '*.tar.gz'
        sh 'rm -rf *'
      }
    }

  }
}