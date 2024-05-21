pipeline {
    agent any
    stages {
        stage('Pull from SCM') {
            steps {
            git branch: 'main', 
            url: 'https://github.com/rajdevops12/react',
            credentialsId: 'Github_Integration' 
            }
        }
        stage('Stop Running Container') {
            steps {
                sh 'docker stop $(docker ps -a -q --filter ancestor=reactproject)'
            }
        }
        stage('Remove Previous Image') {
            steps {
                sh 'docker rmi -f reactproject || true'
            }
        }

        stage('Remove Previous Container') {
            steps {
                sh 'docker rm -f $(docker ps -a -q --filter name=react) || true'
            }
        }

        stage('Build New Image') {
            steps {
                sh 'docker build -t reactproject .'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d --name react -p 4000:80 reactproject'
                sh 'docker buildx prune --force'
            }
        }
    }
}
