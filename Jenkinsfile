pipeline {
  agent any
  stages {
    stage('start') {
      steps {
        script {
        cleanWs()
        git branch: env.BRANCH_NAME, credentialsId: 'dina-cred-github', url: scm.userRemoteConfigs[0].url
        withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
          sh """
              docker login -u ${USERNAME} -p ${PASSWORD}
              docker build -t abosaeed/jenkins_worker .
              docker push abosaeed/jenkins_worker
          """
        }
        
      }
      }
    }
  }
}
