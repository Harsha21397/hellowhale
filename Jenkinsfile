pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git credentialsId: '29b3d4cb-9d60-46d4-963e-bfdef4c3fe5d', url: 'https://github.com/Harsha21397/hellowhale.git'
      }
    }
    
      stage("Build image") {
            steps {
                script {
                   myapp = docker.build("harsha2018/hellowhale:${env.BUILD_ID}")
                     
                }
            }
        }
    
      stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "hellowhale.yml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
