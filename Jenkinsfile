pipeline {
    agent any
    tools {
        jdk 'jdk17'
        nodejs 'node16'
    }
    stages {
        stage ("Clean Workspace") {
            steps {
                cleanWs()
            }
        }
        stage ("Git Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/vikash93825/Starbucks-Application.git'
            }
        }
        stage("Install NPM Dependencies") {
            steps {
                sh "npm install"
            }
        }
        stage("Build Docker Image") {
            steps {
                sh "docker build -t starbucks ."
            }
        }
        stage("Tag & Push to DockerHub") {
            steps {
                script {
                    withDockerRegistry(credentialsId: '38dddd89-2195-4343-a9fd-7e1c58bdee49') {
                        sh "docker tag starbucks vikash43cloud/starbucks:latest"
                        sh "docker push vikash43cloud/starbucks:latest"
                    }
                }
            }
        }
    }
}
