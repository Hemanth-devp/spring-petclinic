pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Hemanth-devp/spring-petclinic.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'docker build -f /home/ec2-user/docker/dockerfile -t myapp .'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image('myapp').inside {
                        sh 'mvn test'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.image('myapp').push('latest')
                    sh 'docker run -d -p 8081:8080 myapp'
                }
            }
        }
    }
}
