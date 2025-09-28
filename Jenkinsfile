@Library("Shared") _

pipeline {
    agent { label 'vinod' }

    stages {
        stage('Hello') {
            steps {
                script {
                    hello()
                }
            }
        }

        stage('Code') {
            steps {
                script {
                    clone('https://github.com/bashairfan0911/django-notes-app.git', 'main')
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    docker_build("notes-app", "latest", env.dockerHubUser)
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker_push("notes-app", "latest", env.dockerHubUser)
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "done dosto"
                    sh "docker compose down || true"
                    sh "docker compose up -d"
                }
            }
        }
    }
}
