pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID     = credentials('Access_Key')
        AWS_SECRET_ACCESS_KEY = credentials('Secret_key')
    }
    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/imrankhanmohammad257/terraform.git', branch: 'main'
            }
        }
        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Terraform Plan') {
            steps {
                sh 'terraform plan'
            }
        }
        stage('Terraform Apply') {
            steps {
                sh 'terraform apply --auto-approve'
            }
        }
    }
}
