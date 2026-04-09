pipeline {
    agent any

    tools {
        maven 'MyMaven'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vikiccha2105-cpu/MyMavenApp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        // ❗ Optional (safe version)
        stage('Run Application') {
            steps {
                sh 'nohup java -jar target/MyMavenApp-1.0-SNAPSHOT.jar &'
            }
        }
    }

    post {
        success {
            echo 'Build successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
