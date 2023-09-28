pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'compiling sysfoo app...'
        sh 'mvn compile'
      }
    }

    stage('test') {
      parallel {
        stage('unit test') {
          steps {
            echo 'running unit tests...'
            sh 'mvn clean test'
          }
        }

        stage('SCA') {
          steps {
            echo 'Software Component Analysis'
            sleep 5
          }
        }

        stage('SAST') {
          steps {
            sleep 9
          }
        }

      }
    }

    stage('package') {
      steps {
        echo 'generating artifact.....'
        sh 'mvn package -DskipTests'
        archiveArtifacts '**/target/*.war'
      }
    }

    stage('container image') {
      steps {
        sleep 5
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}