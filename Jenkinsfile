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
              publishHTML([reportDir: 'build\\reports\\tests\\test', reportFiles: 'index.html', reportName: 'HTML Report'])
          }
      }
      stage('Package') {
            steps {
             sh './gradlew shadowJar'
          }
      }
  }
}
