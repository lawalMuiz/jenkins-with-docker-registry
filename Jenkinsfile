pipeline {
  agent any

  environment {
    SERVICE_NAME       = "jenkins-with-docker-registry"
    ORGANIZATION_NAME  = "lawalmuiz"
    DOCKERHUB_USERNAME = "muizudeen"
    REGISTRY_TAG       = "${DOCKERHUB_USERNAME}/${ORGANIZATION_NAME}-${SERVICE_NAME}:${BUILD_ID}"
  }
  
  stages {

    stage ('Print ENVs') {
      steps {
        sh 'printenv'
      }
    }
    
    stage ('Build Image') {
      steps {
        withDockerRegistry([credentialsId: 'docker-hub', url: ""]) {
          sh 'docker build -t ${REGISTRY_TAG} .'
          sh 'docker push ${REGISTRY_TAG}'
        }
      }
    }
    stage ('Delete Images') {
      steps {
        sh 'docker rmi -f $(docker images -qa)'
      }
    }
  }
}
