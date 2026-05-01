pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Saksh-says/assignment7.git', credentialsId: 'bhoomicred'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the image with your Docker Hub repo name directly
                sh 'docker build -t bhoomiiiiiii/helloapp:v1 .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'bhoomicred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push bhoomiiiiiii/helloapp:v1'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                // Run the image you just pushed
                sh 'docker run --rm bhoomiiiiiii/helloapp:v1'
            }
        }
	stage('Deploy to Kubernetes') {
            steps {
                // Apply deployment and service YAMLs
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }	
	stage('Verify Pod') {
            steps {
                // Check pod status
                sh 'kubectl get pods -l app=hello'
            }
        }

    }

}

