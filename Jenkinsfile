pipeline {
    agent any

    stages {
        stage('Deploy HTML') {
            steps {
                sshagent(['apache']) {
                    script {
                        echo 'Deploying index.html to remote Apache server...'

                        // Ensure the known_hosts file is available
                        sh '''
                        mkdir -p ~/.ssh
                        echo "ip-51-20-115-40 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAt+d6X8+aInVs...your_public_key..." >> ~/.ssh/known_hosts
                        chmod 644 ~/.ssh/known_hosts
                        '''

                        // Copy the file to the remote server
                        sh 'scp index.html ubuntu@ip-51-20-115-40:/var/www/html/'
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
