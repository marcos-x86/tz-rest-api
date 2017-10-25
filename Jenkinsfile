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
    stage('CodeQuality') {
      steps {
        sh './gradlew sonarqube -Dsonar.host.url=http://sonarqube:9000'
      }
    }
    stage('Package') {
      steps {
        sh './gradlew shadowJar'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'example.yml'
      }
    }
  }
  post {
    always {
      junit 'build/test-results/test/*'
    }
  }
}
