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
                 ansible-playbook -i ./roles/my_elasticsearch_role/aws_ec2.yaml ./roles/my_elasticsearch_role/playbook.yml --private-key /var/lib/jenkins/workspace/es_pipeline/infra_key.pem 
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
