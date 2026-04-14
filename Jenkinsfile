pipeline {
    agent any

    tools {
        maven 'MyMaven'
    }

    stages {

        // ❗ REMOVE manual checkout (Jenkins already does it)
        // If you still want manual control, fix branch to 'master'

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

        stage('Run Application') {
            steps {
                sh '''
                if pgrep -f MyMavenApp.jar; then
                    echo "App already running"
                else
                    nohup java -jar target/*.jar > app.log 2>&1 &
                fi
                '''
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
