pipeline{

    agent any

    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub-cred')
        VERSION = "${env.BUILD_ID}"
    }

    stages {

        stage('Build') {

            steps {
                sh 'docker build -t mayuryes99/opstree-task:${VERSION} .'
            }
        }

        stage('Login') {

            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push') {

            steps {
                sh 'docker push mayuryes99/opstree-task:${VERSION}'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }


