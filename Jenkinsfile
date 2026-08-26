pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh './mvnw test'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t product-service:${BUILD_NUMBER} .'
                sh 'docker tag product-service:${BUILD_NUMBER} product-service:latest'
            }
        }
    }

    post {
        success {
            echo 'Product Service CI Pipeline completed successfully!'
        }

        failure {
            echo 'Product Service CI Pipeline failed!'
        }
    }
}