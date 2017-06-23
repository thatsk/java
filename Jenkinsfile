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
    stage('Compile') {
      steps {
        sh 'mvn compile'
      }
    }
    stage('test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Archive') {
      steps {
        junit(allowEmptyResults: true, testResults: '**/target/**/TEST*.xml')
      }
    }
    stage('Uploading Repo') {
      steps {
        echo 'Want tp Upload it func-cp repo'
        input(message: 'Upload it to func-cp repo', ok: 'click to yes', submitter: '123', submitterParameter: '1234')
      }
    }
  }
  post {
    always {
      echo 'deleting workspace'
      deleteDir()
      
    }
    
    success {
      echo 'The build has been succeeded!'
      
    }
    
    unstable {
      echo 'The build has been unstable Please check the build logs:/'
      
    }
    
    failure {
      echo 'Oops the build has been failed :('
      mail(to: 'team@example.com', subject: "Failed Pipeline: ${currentBuild.fullDisplayName}", body: "Something is wrong with ${env.BUILD_URL}")
      
    }
    
  }
}