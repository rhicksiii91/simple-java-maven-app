pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "***BUILD START***"'
                sh 'mvn -B -DskipTests clean package'
                sh 'echo "***BUILD DONE***"'
            }
        }
        stage('Test') {
          steps {
            sh 'echo "SNYK TEST START"'
            sh 'node -v'
            sh 'npm prune'
            sh 'npm install'
            sh 'snyk test'
            sh 'echo "SNYK TEST DONE"'
          }
        }

      }
      environment {
        SNYK_TOKEN = credentials('3e7b6d8a-6db9-4059-b0bd-115af2f9af6d')
}
}