pipeline {
  agent {
    docker {
      image 'maven:3.6.3-jdk-11-slim'
    }

  }
  stages {
    stage('build') {
      steps {
        echo 'compiling sysfoo app...'
        sh 'mvn compile'
      }
    }

    stage('unit test') {
      steps {
        echo 'running unit tests...'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      steps {
        echo 'generating artifact.....'
        sh 'mvn package -DskipTests'
        archiveArtifacts '**/target/*.war'
      }
    }

  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}