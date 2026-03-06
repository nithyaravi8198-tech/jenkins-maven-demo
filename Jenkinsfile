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

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            sh '''
            curl -X POST -H 'Content-type: application/json' \
            --data '{"text":"Jenkins Build SUCCESS: ${JOB_NAME} #${BUILD_NUMBER}"}' \
            https://hooks.slack.com/services/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
            '''
        }
    }
}