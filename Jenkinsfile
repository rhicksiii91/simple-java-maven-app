pipeline {
    agent any
        tools
            {
            nodejs 'NodeJS 8.14.0'
            maven 'maven 3.6.0'
            }

            environment {
                    SNYK_TOKEN = credentials('SNYK_TOKEN')
                }
    stages {
        stage('Install and Authenticate Snyk') {
              steps {
                sh 'node -v'
                sh 'npm prune'
                sh 'npm install -g snyk'
                sh 'snyk auth 3e7b6d8a-6db9-4059-b0bd-115af2f9af6d'
              }
            }

        stage('Build') {
            steps {
                sh 'echo "***BUILD START***"'
                sh 'mvn -B -DskipTests clean package'
                sh 'echo "***BUILD DONE***"'
            }
        }
        stage('Snyk Test') {
                    steps {
                        sh 'echo "***RUNNING SNYK TEST***"'
                        sh 'snyk test'
                    }
                }



     }
    }
