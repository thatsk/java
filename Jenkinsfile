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
    
  }
  post {
    always {
      echo 'deleting workspace'
      deleteDir()
       archive "target/**/*"
       junit 'target/surefire-reports/*.xml'
          
    }
    
    success {
      echo 'The build has been succeeded!'
      
    }
    
    unstable {
      echo 'The build has been unstable Please check the build logs:/'
      
    }
    
    failure {
      echo 'Oops the build has been failed :('
      mail(to: 'bits.kunalsing@gmail.com', subject: "Failed Pipeline: ${currentBuild.fullDisplayName}", body: "Something is wrong with ${env.BUILD_URL}")
      
    }
    
  }
}
