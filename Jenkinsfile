pipeline {

    agent any

    stages {

         stage('Init') {

            steps {

                sh 'docker rm -f $(docker ps -qa) || true'

                sh 'docker network create new-network || true'

            }

        }

        stage('Build') {

            steps {

                sh 'docker build -t faizashahid/fsapp .'

                sh 'docker build -t faizashahid/mynginx ./nginx'

            }

        }
        
        stage('Push') {

            steps {

                sh '''
                docker push faizashahid/fsapp

                docker push faizashahid/mynginx
                '''
            }

        }

        stage('Deploy') {

            steps {

                sh 'docker run -d --name fsapp --network new-network faizashahid/fsapp:latest'

                sh 'docker run -d -p 80:80 --name mynginx --network new-network faizashahid/mynginx:latest'

            }

        }

    }

}