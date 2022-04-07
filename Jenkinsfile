pipeline {
  agent { dockerfile true }
   stages {
    stage('Preparation') {
      steps {
        checkout scm
      }
    }
    stage('docker build/push') {
      steps {
        script {
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
