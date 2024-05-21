pipeline {
    agent any
    
    stages {
        stage('Build and Run Docker Container') {
            steps {
                script {
                    sh 'docker ps -a -q --filter ancestor=reactproject | xargs -r docker rm -f'
                    
                    sh 'docker build -t reactproject .'
                    
                    sh 'docker run -d --name react -p 80:4500 reactproject'
                }
            }
        }
    }
}
