pipeline {
  agent {
    docker {
      image 'bitwiseman/training-blueocean-sample'
      args '-u root -v $HOME/.m2:/root/.m2'
    }
    
  }
  stages {
    stage('Build') {
      steps {
        sh './jenkins/build.sh'
        archiveArtifacts 'target/*.war'
      }
    }
    stage('Test') {
      steps {
        sh './jenkins/test-all.sh'
        junit '**/surefire-reports/**/*.xml'
        junit '**/test-results/karma/*.xml'
      }
    }
    stage('Deploy') {
      steps {
        sh './jenkins/deploy.sh dev'
      }
    }
    stage('Deploy to Staging') {
      steps {
        input 'Deploy to Staging'
      }
    }
  }
}