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
            sh 'chmod +x gradlew'
            sh './gradlew clean build'
            }
        }

        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }

        stage('Verify Build Output') {
            steps {
                sh 'ls app/build/libs'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t cicd-app .'
            }
        }

        stage('Run') {
            steps {
                sh 'docker rm -f cicd-app || true'
                sh 'docker run -d --name cicd-app cicd-app'
            }
        }
    }
}