pipeline {
    agent any

    tools {
        maven 'Maven'   // Use your configured Maven tool name
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/nithyaravi8198-tech/jenkins-maven-demo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}