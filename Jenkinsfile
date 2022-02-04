pipeline {
  environment {
    registry = 'mariaguti30/dockerjenkins1'
    registryCredential = 'MyDockerID'
    dockerImage = 'Dockerfile'
  }
  agent any
  stages {
    stage ("Clone Git Project") {
      steps {
        git url: 'https://github.com/mariaguti30/dockerjenkins1.git'
      }
    }
    stage ("Build and test code project") {
      steps {
        sh 'pwd'
        sh 'ls -l'
        sh 'java -version'
        sh 'javac HelloJava.java'
        sh 'java HelloJava'
      }
    }
    stage ("Building image") {
        steps{
            script {
                dockerImage = docker.build registry + ":b$BUILD_NUMBER"
            }
        }
    }
    stage ("Deploy Image") {
        steps {
            script {
                docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                }
            }
        }
    }
  }
}

