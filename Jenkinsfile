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
                sh './gradlew clean build'
            }
        }

        stage('Verify JAR') {
            steps {
                sh 'ls build/libs'
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