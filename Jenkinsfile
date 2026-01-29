pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    echo "Stopping old Spring Boot app..."
                    pkill -f ".jar" || true

                    echo "Starting new Spring Boot app..."
                    nohup java -jar target/*.jar > app.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Build & deploy completed"
        }
        failure {
            echo "❌ Pipeline failed"
        }
    }
}
