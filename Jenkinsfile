def COLOR_MAP = [
    'SUCCESS': 'good',
    'FAILURE': 'danger'
    ]

pipeline {
    agent any

    stages {
        stage('Fetch') {
            steps {
                sh 'https://github.com/suhas-14/docker-test.git'
            }
        }
        stage('Docker Compose') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-key', toolName: 'docker') {
                        sh 'sudo docker compose up -d'
                    }
                }
            }
        }
        stage('Result') {
            steps {
                echo 'success'
        }
    }
    }
    post {
        always {
        echo 'Slack Notification'
        slackSend channel: '#ci-cd-pipeline',
        color: COLOR_MAP [currentBuil.current.Result],
        message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} Build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}"
        }        
    }
}
