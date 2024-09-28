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

        // Uncomment if you need to install Ansible and AWS dependencies on the Jenkins node
        /*
        stage('Install Ansible and AWS dependencies') {
            steps {
                sh '''
                sudo apt update
                sudo apt install ansible python3-pip -y
                pip install boto3 --break-system-packages
                '''
            }
        }
        */

        stage('Run Ansible Playbook') {
            steps {
                // List files in the workspace to check if everything is in place
                sh 'ls -al'
                
                // Change permissions of the private key
                sh '''
                chmod 400 /var/lib/jenkins/workspace/es_pipeline/infra_key.pem
                '''

                // Run the Ansible playbook with the specified private key and inventory file
                sh '''
                 ansible-playbook -i ./roles/my_elasticsearch_role/aws_ec2.yaml \
                ./roles/my_elasticsearch_role/playbook.yml 
                # --private-key /var/lib/jenkins/workspace/es_pipeline/infra_key.pem 
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
