pipeline {
    agent any

    tools {
        terraform 'Terraform'   // The name you configured in Jenkins Tools
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
                sh 'terraform init()'
            }
        }

        stage('Terraform Plan') {
            steps {
                terraform plan()
            }
        }

        stage('Terraform Apply') {
            steps {
                input(message: "Do you want to apply Terraform changes?") // manual approval
                terraform apply()
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
