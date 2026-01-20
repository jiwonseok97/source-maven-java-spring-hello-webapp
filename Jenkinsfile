pipeline {
  agent any

  triggers {
    pollSCM('H/1 * * * *')
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main',
            url: 'https://github.com/jiwonseok97/source-maven-java-spring-hello-webapp.git'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn -B clean package'
      }
    }

    stage('Deploy') {
      steps {
        deploy adapters: [
          tomcat9(
            credentialsId: 'tomcat',
            url: 'http://192.168.56.102:8080'
          )
        ],
        contextPath: '',
        war: 'target/hello-world.war'
      }
    }
  }
}

