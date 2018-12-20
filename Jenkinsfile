pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }

        tools
            {
            nodejs 'NodeJS 8.14.0'
            }

            environment {
                    SNYK_TOKEN = credentials('0b2eaa21-0a45-4d71-83ed-bb77713c656d')
                }

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
            sh 'snyk auth 0b2eaa21-0a45-4d71-83ed-bb77713c656d'
            sh 'snyk test'
          }
        }
     }
    }
