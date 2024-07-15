def COLOR_MAP = [
    'SUCCESS': 'good',
    'FAILURE': 'danger'
    ]
pipeline {
    agent any
    stages {
        stage('git checkout') {
            steps {
             git 'https://github.com/suhas-14/docker-test.git'
            }
        }
        stage('docker compose') {
            steps {
             script {
                 withDockerRegistry(credentialsId: 'docker-key', toolName: 'docker') {
                    sh 'docker-compose up -d'
                  }
              }
            }
        }
    }	
 
    post {
        always {
            echo 'slack Notification.'
            slackSend channel: '#ci-cd-pipeline',
            color: COLOR_MAP [currentBuild.currentResult],
            message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URl}"  
        }
    }
}
