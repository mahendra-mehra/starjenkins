pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Build helloworld app'
        build 'java-app'
      }
    }

    stage('linux test') {
      parallel {
        stage('linux test') {
          steps {
            echo 'run example2 shell'
            sh 'sh example2.sh'
          }
        }

        stage('windows test') {
          steps {
            echo 'this is windowss test'
          }
        }

      }
    }

    stage('deploy at staging') {
      steps {
        echo 'Deploy to staging environment'
        input 'Ok to deploy to production? '
      }
    }

    stage('Deploy Production stage') {
      steps {
        echo 'deploy to prod server'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/java-app.jar', fingerprint: true)
    }

    failure {
      mail(to: 'probuster@gmail.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}