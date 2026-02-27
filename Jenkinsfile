pipeline {
    agent any

    tools {
        maven 'Maven-3'   
        jdk 'Java-17'     
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Diego20251/Exp3_S8_Diego_Paredes_Springboot-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }
}