pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
        node {
          echo "DOCKER STAGE DONE!"
        }

    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
            node {
                      echo "PACKAGE BUILT!"
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

      }
      node {
                echo "SNYK TEST HAS BEEN RUN!"
              }
      environment {
        SNYK_TOKEN = credentials('3e7b6d8a-6db9-4059-b0bd-115af2f9af6d')
}
}