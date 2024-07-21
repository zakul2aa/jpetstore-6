pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'First Jenkins'
        sh './mvnw clean compile'
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw test'
        junit '**/target/surefire-reports/TEST-*.xml'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.projectKey=JPetstore \\
  -Dsonar.projectName=\'JPetstore\' \\
  -Dsonar.host.url=http://13.200.143.107:9000 \\
  -Dsonar.token=sqp_069fcdbfd83932f92ef7a5236ecb843f522e4d8c'''
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
      }
    }

  }
}