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
        stage('Install Snyk') {
              steps {
                sh 'node -v'
                sh 'npm prune'
                sh 'npm install -g snyk'
              }
            }

        stage('Build') {
            steps {
                sh 'echo "***BUILD START***"'
                sh 'mvn -B -DskipTests clean install'
                sh 'echo "***BUILD DONE***"'
            }
        }
        stage('Snyk Test') {
                    steps {
                        sh 'echo "***RUNNING SNYK TEST***"'
                        sh 'snyk test --file=pom.xml'
                    }
                }

        stage('Snyk Monitor') {
                            steps {
                                sh 'echo "***RUNNING SNYK TEST***"'
                                sh 'snyk monitor --file=pom.xml --org=0e87a59b-680e-44ad-a33e-9999d62d8469'
                            }
                        }

     }
    }
