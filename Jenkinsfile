pipeline {   
  agent {
        docker {
            image 'hashicorp/terraform:light'
            label 'master'
            args  '--entrypoint="" -v /root/jenkins/jenkins_home/.aws:/root/.aws'
        }
  }
  stages {
    stage('init') {
      steps {
        sh 'terraform init -input=false'
      }
    }
    stage('approval_plan') {
      steps {
        input 'approve the init to proceed and plan'
      }
    }
    stage('plan') {
      steps {
        sh 'terraform plan -out tfapply'
      }
    }
    stage('approval_apply') {
      options {
        timeout(time: 1, unit: 'HOURS') 
      }
      steps {
        input 'approve the plan to proceed and apply'
      }
    }
    stage('apply') {
      steps {
        sh 'terraform apply -auto-approve tfapply'
        cleanWs()
      }
    }
  }
}
