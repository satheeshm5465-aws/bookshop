pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/satheeshm5465-aws/bookshop'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@<EC2-IP> << EOF
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
