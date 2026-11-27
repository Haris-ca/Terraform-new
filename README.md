# Terraform-new


pipeline{
    agent{
        label 'Terraform'
    }
    stages{
        stage('init'){
            steps{
                 deleteDir()
                sh '''
                    
                    git clone  https://github.com/Haris-ca/Terraform-new.git
                    cd Terraform-new
                    terraform init
                '''
            }
        }
        stage('plan'){
            steps{
                sh '''
                    cd Terraform-new
                    terraform plan
                '''
            }
        }
        stage('approval'){
            steps{
                input message: 'Apply terraform plan?', ok: 'Yes, apply'
            }
        }
        stage('apply'){
            steps{
                sh '''
                    cd Terraform-new
                    terraform apply -auto-approve
                '''
            }
        }
    }
}
