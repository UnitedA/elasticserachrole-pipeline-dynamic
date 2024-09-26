pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/UnitedA/elasticserachrole-pipeline-dynamic.git'
            }
        }
        // stage('Install Ansible and AWS dependencies') {
        //     steps {
        //         sh '''
        //         sudo apt update
        //         sudo apt install ansible python3-pip -y
        //         pip install boto3 --break-system-packages
        //         '''
        //     }
        // }
        stage('Run Ansible Playbook') {
            steps {
                sh 'ls -al'
                sh '''
                ansible-playbook -i ./roles/my_elasticsearch_role/aws_ec2.yml ./roles/my_elasticsearch_role/playbook.yml
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
