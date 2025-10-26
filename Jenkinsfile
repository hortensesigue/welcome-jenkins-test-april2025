pipeline {
    agent any
    environment {
        DOCKERHUB_REPO = 'hortensehouendji/welcome-jenkins-test'
        DOCKERHUB_CREDS     = credentials('dockerhubCreds-id')
    }

    stages {
        stage('Source') {
            steps {
                echo 'checking into github'
                git branch: 'main', credentialsId: 'GithubCreds-id', url: 'https://github.com/hortensesigue/welcome-jenkins-test-april2025.git'
            }
        }
        stage('Build') {
            steps {
                echo 'building the docker image'
                sh 'docker build -t ${DOCKERHUB_REPO}:v${BUILD_NUMBER} .'
            }
        }
        stage('Deploy') {
            steps {
                echo 'login into dockerhub'
                sh 'docker login -u ${DOCKERHUB_CREDS_USR} -p ${DOCKERHUB_CREDS_PSW}'
                echo 'deploying the docker image to dockerhub'
                sh 'docker push ${DOCKERHUB_REPO}:v${BUILD_NUMBER}'
            }
        }
    }
}
