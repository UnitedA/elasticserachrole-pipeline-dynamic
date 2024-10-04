pipeline {
    agent any
    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/UnitedA/elasticserachrole-pipeline-dynamic.git'
            }
        }

        stage('Run Playbook') {
            steps {
                sh '''
                chmod 400 /var/lib/jenkins/tool.pem
                ansible-playbook -i aws_ec2.yaml playbook.yml --private-key /var/lib/jenkins/tool.pem -vvvv
                ansible-playbook -i aws_ec2.yaml kibana.yml --private-key /home/aryan/all_key.pem -vvvv
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
