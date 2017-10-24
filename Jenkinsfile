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
        publishHTML target: [
          allowMissing: false,
          alwaysLinkToLastBuild: false,
          keepAll: true,
          reportDir: 'build/reports/tests/test/',
          reportFiles: 'index.html',
          reportName: 'Tests Report'
        ]
      }
    }
    stage('Package') {
      steps {
        sh './gradlew shadowJar'
        archiveArtifacts 'build/libs/*.jar'
      }
    }
  }
}
