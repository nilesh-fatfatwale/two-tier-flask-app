pipeline {
    agent {label "dev"};

    stages {
        stage("Code") {
            steps {
                git url: "https://github.com/nilesh-fatfatwale/two-tier-flask-app", branch: "main"
            }
        }

        stage("Build") {
            steps {
                sh "docker build -t flask-app:latest ."
            }
        }

        stage("Test") {
            steps {
                echo "code is testing"
            }
        }

        stage("Push to Docker Hub") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "dockerHubCreds",
                    usernameVariable: "DOCKER_USERNAME",
                    passwordVariable: "DOCKER_PASSWORD"
                )]) {
                    sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
                    sh "docker image tag flask-app $DOCKER_USERNAME/flask-app"
                    sh "docker push $DOCKER_USERNAME/flask-app:latest"
                }
            }
        }

        stage("Run") {
            steps {
                sh "docker compose up -d --build flask-app"
            }
        }
    }
}
