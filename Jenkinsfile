pipeline {
  agent 'any'
  stages {
    stage('CodeCommit') {
      steps {
        sh './gradlew clean assemble'
      }
    }
    stage('Test') {
      steps {
        sh './gradlew clean check'
      }
    }
    stage('Package') {
      steps {
        sh './gradlew shadowJar'
      }
    }
  }
}
