pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Using a Docker container for the build process
                    docker.image('node:18-alpine').inside('-v c:/data/jenkins_home/workspace:/workspace') {
                        // Change to the workspace directory
                        bat 'cd /workspace'
                        bat 'node --version'
                        bat 'npm --version'
                        bat 'npm ci'
                        bat 'npm run build'
                        bat 'dir'
                    }
                }
            }
        }

        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }

