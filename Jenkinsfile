pipeline {
    agent any

    tools {
        terraform 'Terraform-1.13.1'   // name from Manage Jenkins > Tools
    }

    environment {
        AWS_DEFAULT_REGION = "us-east-1"
    }

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/imrankhanmohammad257/terraform.git'
            }
        }

        stage('Terraform Init') {
            steps {
                script {
                    def tfHome = tool name: 'Terraform-1.13.1', type: 'org.jenkinsci.plugins.terraform.TerraformInstallation'
                    env.PATH = "${tfHome}:${env.PATH}"
                }
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Terraform Apply') {
            steps {
                input message: "Do you want to apply Terraform changes?"
                sh 'terraform apply -auto-approve tfplan'
            }
        }
    }

    post {
        success {
            echo "✅ Terraform pipeline executed successfully!"
        }
        failure {
            echo "❌ Terraform pipeline failed!"
        }
    }
}
