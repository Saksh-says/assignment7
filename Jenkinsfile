pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Saksh-says/assignment7.git', credentialsId: 'Saksh1997'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t hello-world-java .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run --rm hello-world-java'
                }
            }
        }
    }
}

