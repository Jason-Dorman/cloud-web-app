pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('Clone repository') {
            steps {
                script{
                checkout scm
                }
            }
        }

        stage('Build') {
            steps {
                script{
                 app = docker.build("movie-app")
                }
            }
        }
        stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
        stage('Deploy') {
            steps {
                script{
                        docker.withRegistry('https://243764803067.dkr.ecr.us-west-2.amazonaws.com/movie-app', 'ecr:us-west-2:aws-credentials-west') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    // docker.image("movie-app").push()
                    }
                }
            }
        }
    }
}
