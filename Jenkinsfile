pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_TAG', defaultValue: 'v2', description: 'Docker image tag to deploy')
    }

    environment {
        DOCKER_IMAGE = "rberry009/assignment-2-app"
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Deploy with Ansible') {
            steps {
                sh '''
                    ansible-playbook -i inventory.ini playbook.yml \
                    --extra-vars "docker_image=${DOCKER_IMAGE}:${IMAGE_TAG}"
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                    curl http://34.201.220.5
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment completed successfully."
        }
        failure {
            echo "Deployment failed."
        }
    }
}