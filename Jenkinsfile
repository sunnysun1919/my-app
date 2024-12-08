pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'my-app:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'git@github.com:sunnysun1919/my-app.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
                // 这里可以添加具体的测试命令
            }
        }

        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/repositories/sunnysun1919', 'docker-hub-credentials') {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
