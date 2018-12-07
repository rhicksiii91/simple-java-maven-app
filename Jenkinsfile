pipeline {
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
            sh 'node -v'
            sh 'npm prune'
            sh 'npm install'
            sh 'snyk test'
          }
        }
        stage('Run Snyk Test') {
          steps {
            sh 'snyk monitor'
          }
        }
     }
      environment {
                    SNYK_TOKEN = credentials('3e7b6d8a-6db9-4059-b0bd-115af2f9af6d')
                  }
    }
