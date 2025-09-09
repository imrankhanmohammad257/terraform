pipeline {
    agent any

    tools {
        terraform 'Terraform-1.13.1'   // The name you configured in Jenkins Tools
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
                terraformInit()
            }
        }

        stage('Terraform Plan') {
            steps {
                terraformPlan()
            }
        }

        stage('Terraform Apply') {
            steps {
                input(message: "Do you want to apply Terraform changes?") // manual approval
                terraformApply()
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
