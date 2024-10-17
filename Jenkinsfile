pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                //    docker.image('node:18-alpine').inside('-v c:\\data\\jenkins_home\\workspace\\Udemy_Task:/workspace') {
                    docker run -d \
  -p 8080:8080 \
  -v c:/data/jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts
                        bat 'dir'
                        bat 'node --version'
                        bat 'npm --version'
                        bat 'npm ci'
                        bat 'npm run build'
                        bat 'dir'
                    }
                }
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps {
                script {
                    bat '''
                        if exist build\\index.html (
                            npm test
                        ) else (
                            echo "Build index.html not found"
                            exit 1
                        )
                    '''
                }
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
