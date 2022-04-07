pipeline {
  agent { dockerfile true }
   stages {
    stage('Preparation') {
      steps {
        script {
        checkout scm
        sh "git rev-parse --short HEAD > .git/commit-id"                        
        def commit_id = readFile('.git/commit-id').trim()
        }
      }
    }
    stage('docker build/push') {
      steps {
        script {
        def app = docker.build "moreskovic/demo-asp:${commit_id}"
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
