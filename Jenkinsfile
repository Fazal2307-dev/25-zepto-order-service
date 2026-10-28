pipeline {
    agent any

    environment {
        DB_PASSWORD = credentials('zepto-db-password')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Fazal2307-dev/25-zepto-order-service.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t zepto-order-service .'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker rm -f zepto-order-service >nul 2>&1 || ver >nul'
                bat "docker run -d -p 8081:8081 --name zepto-order-service -e SPRING_DATASOURCE_URL=jdbc:mysql://host.docker.internal:3306/9th_march_kodewala_academy -e DB_PASSWORD=${DB_PASSWORD} zepto-order-service"
            }
        }
    }
}
