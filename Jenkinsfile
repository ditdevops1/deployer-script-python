pipeline {
    agent any


    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/ditdevops1/deployer-script-python.git'
            }
        }


        stage('Run Script') {
            steps {
                bat 'python app.py'
            }
        }

        stage('Notify') {
            steps {
                script {
                    def result = currentBuild.result ?: 'SUCCESS'
                    emailext subject: "Jenkins Build: ${result}",
                        body: "Build Status: ${result}\nVoir Jenkins: ${env.BUILD_URL}",
                        to: 'ditdevops1@gmail.com'
                }
            }
        }
    }

    post {
        failure {
            emailext subject: "Échec du build Jenkins",
                body: "Échec du pipeline : ${env.BUILD_URL}",
                to: 'ditdevops1@gmail.com'
        }
    }
}