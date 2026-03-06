pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }

    }

    post {
        success {
            withCredentials([string(credentialsId: 'slack-webhook', variable: 'SLACK_WEBHOOK')]) {
                sh """
                curl -X POST -H 'Content-type: application/json' \
                --data '{\"text\":\"Jenkins Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}\"}' \
                \$SLACK_WEBHOOK
                """
            }
        }

        failure {
            withCredentials([string(credentialsId: 'slack-webhook', variable: 'SLACK_WEBHOOK')]) {
                sh """
                curl -X POST -H 'Content-type: application/json' \
                --data '{\"text\":\"Jenkins Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}\"}' \
                \$SLACK_WEBHOOK
                """
            }
        }
    }
}