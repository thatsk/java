pipeline {
  agent {
    node {
      label 'maven'
    }
    
  }
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/thatsk/java.git', branch: 'master', changelog: true)
      }
    }
    stage('test ') {
      steps {
        sh 'mvn test'
      }
    }
    stage('cleaning up workspace') {
      steps {
        cleanWs(cleanWhenSuccess: true)
      }
    }
    stage('Upload to func?') {
      steps {
        echo 'Upload to it func-cp repo'
        input(message: 'Upload it to func-cp repo', ok: 'yes')
      }
    }
  }
}