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
                script{withCredentials([string(credentialsId: 'dockerhub-pass', variable: 'docker_password')]) {
                    sh 'docker login -u mayuryes99 -p $docker_password'
                        }           

                    }
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
}
