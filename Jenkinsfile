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
        stage('Docker Build') {
            steps {
                sh 'docker build -t springbootapp .'
            }
        }
        stage('Docker Run') {
            steps {
                sh '''
                docker stop springbootapp || true
                docker rm springbootapp || true
                docker run -d -p 9090:8080 --name springbootapp \
                  -e SPRING_DATASOURCE_URL=jdbc:postgresql://database-1.cojihkoxovqd.us-east-1.rds.amazonaws.com:5432/springboot_db \
                  -e SPRING_DATASOURCE_USERNAME=postgres \
                  -e SPRING_DATASOURCE_PASSWORD=SpringPass2026! \
                  springbootapp
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline finalizado. Contenedores activos:'
            sh 'docker ps -a'
        }
    }
}
