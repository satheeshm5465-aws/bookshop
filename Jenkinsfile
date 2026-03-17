pipeline {
    agent any

    stages {

        stage('Deploy to EC2') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'ec2-key', keyFileVariable: 'SSH_KEY', usernameVariable: 'USER')]) {
                    sh '''
                    chmod 400 $SSH_KEY

                    ssh -i $SSH_KEY -o StrictHostKeyChecking=no $USER@43.205.124.178 << EOF
                    sudo rm -rf /var/www/html/*
                    sudo cp -r * /var/www/html/
                    sudo systemctl restart apache2
                    EOF
                    '''
                }
            }
        }
    }
}
