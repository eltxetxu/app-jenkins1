pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t app:test .'
            }
        }
        stage('Test') {
            steps { 
                echo 'TEST':
                sh 'docker run --rm --name app -id -p 80:80 app:test'
                sh '/bin/nc -vz localhost 80'
            }
            post {
                always {
                    sh 'docker container stop app'
                }
            }
        }
        stage('Push registry') {
            steps {
                echo 'PUSH'
                sh 'docker tag app:test eltxtextu/app:stable'
                sh 'docker push eltxtextu/app:stable'
            }
        }
    }
}