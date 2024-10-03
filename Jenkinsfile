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

        stage('Run Ansible Playbook') {
            steps {
                // Ensure the correct permissions for the private key
                sh '''
                chmod 400 /var/lib/jenkins/.ssh/all_key.pem
                '''

                // Run the Ansible playbook with the specified private key and inventory file
                sh '''
                ansible-playbook -i ./roles/my_elasticsearch_role/aws_ec2.yaml \
                ./roles/my_elasticsearch_role/playbook.yml \
                --private-key /var/lib/jenkins/.ssh/all_key.pem
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
