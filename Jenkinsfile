node {
  git 'https://github.com/devandsecops/content-terraform-docker-service.git'
  stage('init') {
    sh label: 'Initialize Terraform', script: "terraform init"
  }
  stage('plan') {
    sh label: 'Plan Terraform', script: "terraform plan -out=tfplan -input=false -var image_name=${image_name} -var ghost_ext_port=${ghost_ext_port}"
    script {
        timeout(time: 10, unit: 'MINUTES') {
          input(id: "Deploy Gate", message: "Deploy environment?", ok: 'Deploy')
        }
    }
  }
  stage('apply') {
    sh label: 'Deploy Infrastructure', script: "terraform apply -lock=false -input=false tfplan"
  }
}
