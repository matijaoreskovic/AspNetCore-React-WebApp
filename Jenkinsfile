pipeline {
  agent any
   stages {
    stage('Preparation') {
      steps {
          echo 'Priprema....'
      }
    }
    stage('docker build/push') {
      steps {
          echo 'Starting to build docker image'
        script {
            checkout scm
            def app = docker.build("moreskovic/demo-asp:${env.BUILD_ID}")
            docker.withRegistry('https://index.docker.io/v2/', 'DockerHub') {
            app.push()
        }
      }
      }
    }
    stage('kubernetes apply') {
      steps {
        script {
        withKubeConfig([credentialsId: 'k8s_config_BlueOcean']) {
            sh 'kubectl apply -f deploy.yaml -n web'
    }
        }
      }
    }
   }
  
} 
