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
                // Build the image with your Docker Hub repo name directly
                sh 'docker build -t saksh1997/hello11:javav1 .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push saksh1997/hello11:javav1'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                // Run the image you just pushed
                sh 'docker run --rm saksh1997/hello11:javav1'
            }
        }
    }
}

