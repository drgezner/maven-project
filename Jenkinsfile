pipeline {
  /* agent any */
  agent any

  stages {
    stage('Maven clean all and build package') {
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
   
    
    stage ('Deploy to staging') {
      steps {
        build job: 'deploy-artifacts-to-tomcat'
      }
    }
 
    stage ('Deploy to Production') {
      steps{
        timeout(time:5, unit:'MINUTES'{
          input message:'Approve PRODUCTION Deployment?'
        }

        build job: 'deploy-mavenproj-to-prod'
      }
      post{
        success {
          echo 'Code deployed to production.'
        }

        failure {
          echo ' Deployment failed.'
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
