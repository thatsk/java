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
    stage('test') {
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
  post {
        always {
            echo 'deleting workspace'
            deleteDir() /* clean up our workspace */
        }
		success {
            echo 'The build has been succeeded!'
        }
        unstable {
            echo 'The build has been unstable Please check the build logs:/'
        }
        failure {
            echo 'Oops the build has been failed :('
			mail to: 'team@example.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
			}
	}
}
