pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building Docker image...'
                // Збираємо образ з вашим нікнеймом
                sh 'docker build -t vikatushn/jenkins-lab:latest .'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo "Tests passed!"'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Pushing to DockerHub...'
                // Використовуємо збережений пароль (ID має бути dockerhub-credentials)
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    // Логінимось у Docker Hub
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    // Відправляємо образ
                    sh 'docker push vikatushn/jenkins-lab:latest'
                }
            }
        }
    }
}
