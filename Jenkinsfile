pipeline {
  /* agent any */
  agent any

  stages {
    stage('Init') {
      steps {
        sh 'mvn clean package'
      }
      
      post {
        success {
          echo "Now Archiving..."
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }
  } 

}
/*
    stage('Build') {
      steps {
        echo 'Building...'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Code deployed.'
      }
    }
*/
