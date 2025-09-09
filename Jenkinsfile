pipeline {
    agent any

    parameters {
        string(name: 'FILENAME', defaultValue: 'animals.txt', description: 'Name of the file to create')
        string(name: 'CONTENT', defaultValue: 'some animals are human friendly', description: 'Content of the file')
    }

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/imrankhanmohammad257/terraform.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh """
                terraform plan -out=tfplan \
                  -var="filename=${params.FILENAME}" \
                  -var="content=${params.CONTENT}"
                """
            }
        }

        stage('Terraform Apply') {
            steps {
                input message: "⚠️ Do you want to apply Terraform changes?"
                sh 'terraform apply -auto-approve tfplan'
            }
        }
    }

    post {
        success {
            echo "✅ Terraform executed successfully. File: ${params.FILENAME}"
        }
        failure {
            echo "❌ Terraform pipeline failed!"
        }
    }
}
