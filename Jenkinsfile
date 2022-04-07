pipeline {
  agent any
   stages {
    stage('kubernetes apply') {
      steps {
        script {
        withKubeConfig([credentialsId: 'k8s_config_BlueOcean']) {
            sh 'kubectl create pod busybox-test --image=busybox'
    }
        }
      }
    }
   }
  
} 
