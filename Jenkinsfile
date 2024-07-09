pipeline {
  agent { label 'docker-app1' }
  
  stages {
    stage('Prepare') {
      steps {
        script {
          // Move WebApp.war to the target directory
          sh 'sudo mv /home/ubuntu/target/WebApp.war /home/ubuntu/com'
        }
      }
    }
    
    stage('Build Docker Image') {
      steps {
        script {
          // Change directory to /home/ubuntu/com
          dir('/home/ubuntu/com') {
            // Stop and remove existing Docker container if running
            sh 'docker stop mycontainer || true'
            sh 'docker rm mycontainer || true'
            
            // Build new Docker image
            sh 'docker build -t myimage .'
          }
        }
      }
    }
    
    stage('Run Docker Container') {
      steps {
        script {
          // Change directory to /home/ubuntu/com
          dir('/home/ubuntu/com') {
            // Run new Docker container
            sh 'docker run -d --name mycontainer -p 8090:8080 myimage'
          }
        }
      }
    }
  }
  
  post {
    success {
      echo 'Pipeline completed successfully!'
    }
    failure {
      echo 'Pipeline failed!'
    }
  }
}
