pipeline {

  environment {
      registry = "https://hub.docker.com/repository/docker/hcloud203/acp-test/justme/myweb"
      dockerImage = ""
  }
  
  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/hclod203/jc-test.git'
      }
    }
    
     stage('Build Image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
         }
       }
     }
    
    stage('Push Image') {
      steps {
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
         }
       }
     }
   }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
