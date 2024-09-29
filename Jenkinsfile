pipeline {
    agent any
    environment {
        // Disable host key checking for Ansible SSH
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository from GitHub
                git branch: 'main', url: 'https://github.com/UnitedA/elasticserachrole-pipeline-dynamic.git'
            }
        }

        stage('Prepare Environment') {
            steps {
                // List files in the workspace to check if everything is in place
                sh 'ls -al'
                
                // Ensure the correct permissions for the private key
                sh '''
                chmod 400 ~/.ssh/infra_key.pem
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                // Run the Ansible playbook with the specified private key and inventory file
                sh '''
                ansible-playbook -i ./roles/my_elasticsearch_role/aws_ec2.yaml \
                ./roles/my_elasticsearch_role/playbook.yml \
                --private-key ~/.ssh/infra_key.pem
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful'
        }
        failure {
            echo 'Deployment failed'
        }
    }
}
