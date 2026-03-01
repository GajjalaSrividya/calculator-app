pipeline {
    agent any

    // Disable Jenkins default automatic checkout
    options {
        skipDefaultCheckout()
    }

    stages {

        stage('Checkout Code') {
            steps {
                // Explicitly checkout the main branch
                git branch: 'main', url: 'https://github.com/GajjalaSrividya/calculator-app.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('Package JAR') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Install to Local Repo') {
            steps {
                sh 'mvn install'
            }
        }
    }

    post {
        success {
            echo 'Library JAR packaged and installed successfully'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
        failure {
            echo 'Build failed'
        }
    }
}
