pipeline {
    agent any
    stages {
        stage('Pull from SCM') {
            steps {
                script {
                    // Cloning the repository using GitHub credentials
                    echo "Cloning the repository"
                    git branch: 'main', 
                        credentialsId: 'Github_Integration', 
                        url: 'https://github.com/rajdevops12/react.git'
                }
            }
        }
        stage('Stop Running Container') {
            steps {
                script {
                    echo "Stopping any running containers from previous builds"
                    sh 'docker stop $(docker ps -a -q --filter ancestor=reactproject) || true'
                }
            }
        }
        stage('Remove Previous Image') {
            steps {
                script {
                    echo "Removing previous Docker image"
                    sh 'docker rmi -f reactproject || true'
                }
            }
        }
        stage('Remove Previous Container') {
            steps {
                script {
                    echo "Removing previous Docker container"
                    sh 'docker rm -f $(docker ps -a -q --filter name=react) || true'
                }
            }
        }
        stage('Build New Image') {
            steps {
                script {
                    echo "Building new Docker image"
                    sh 'docker build -t reactproject .'
                }
            }
        }
        stage('Run New Container') {
            steps {
                script {
                    echo "Running new Docker container"
                    sh 'docker run -d --name react -p 4000:80 reactproject'
                    sh 'docker buildx prune --force'
                }
            }
        }
    }
}
