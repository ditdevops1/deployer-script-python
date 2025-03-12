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
    }

    post {
        success {
            script {
                emailext subject: "Jenkins Build SUCCESS - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """<p><b>Build SUCCESS</b></p>
                            <p>Job Name: ${env.JOB_NAME}</p>
                            <p>Build Number: ${env.BUILD_NUMBER}</p>
                            <p><a href="${env.BUILD_URL}">Voir le détail</a></p>""",
                    recipientProviders: [[$class: 'RequesterRecipientProvider']],
                    to: 'ditdevops1@gmail.com',
                    mimeType: 'text/html'
            }
        }

        failure {
            script {
                emailext subject: "Jenkins Build FAILURE - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """<p><b>Build FAILURE</b></p>
                            <p>Job Name: ${env.JOB_NAME}</p>
                            <p>Build Number: ${env.BUILD_NUMBER}</p>
                            <p><a href="${env.BUILD_URL}">Voir le détail</a></p>""",
                    recipientProviders: [[$class: 'RequesterRecipientProvider']],
                    to: 'ditdevops1@gmail.com',
                    mimeType: 'text/html'
            }
        }

        always {
            script {
                emailext subject: "Jenkins Build COMPLETED - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """<p><b>Build Completed</b></p>
                            <p>Job Name: ${env.JOB_NAME}</p>
                            <p>Build Number: ${env.BUILD_NUMBER}</p>
                            <p><a href="${env.BUILD_URL}">Voir le détail</a></p>""",
                    recipientProviders: [[$class: 'RequesterRecipientProvider']],
                    to: 'ditdevops1@gmail.com',
                    mimeType: 'text/html'
            }
        }
    }
}
