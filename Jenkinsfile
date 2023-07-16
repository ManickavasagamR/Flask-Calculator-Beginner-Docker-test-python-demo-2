pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh 'echo "building the repo"'
          }
        }
      }
    }

    stage('Test') {
      steps {
        sh 'python test_app.py'
      }
    }

    stage('Deploy')
    {
      steps {
        sh "pip install -r requirements.txt"
        echo "deploying the application"
        sh "pwd"
        sh "hostname"
        echo "killing old python process"
        sh "netstat -tulpn | grep LISTEN"
        sh "whoami"
        echo "initiating new python process"
        sh "sudo nohup python app.py > log.txt 2>&1 &"
        sh "netstat -tulpn | grep LISTEN"
        echo "Flask Application Up and running!"
      }
    }

  }

  post {
        always {
            echo 'The pipeline completed'
            junit allowEmptyResults: true, testResults:'**/test_reports/*.xml'
        }
        success {
            
            echo "app depployment successful"
        }
        failure {
            echo 'Build stage failed'
            error('Stopping early…')
        }
      }
}
