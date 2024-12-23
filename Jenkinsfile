pipeline {
    agent any

    stages {
        stage('Deploy HTML') {
            steps {
                sshagent(['apache']) {
                    script {
                        echo 'Deploying index.html to remote Apache server...'

                        // Copy the file to the remote server
                        sh 'scp index.html ubuntu@ip-172-31-30-135:/var/www/html/'
                    }
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    echo 'Verifying index.html deployment on remote server...'
                    sh 'curl http://ip-51-20-115-40/index.html'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully!'
        }
        failure {
            echo 'Deployment failed. Check the logs for more details.'
        }
    }
}
