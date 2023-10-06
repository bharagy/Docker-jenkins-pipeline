pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t my-flask .'
        sh 'docker tag my-flask $DOCKER_BFLASK_IMAGE'
      }
    }
    /*
    stage('Test') {
      steps {
        sh 'docker run my-flask python -m pytest app/tests/'
      }
    }
    */
    stage('Deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: "${DOCKER_REGISTRY_CREDS}", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
          sh "echo \abcd12345 | docker login -u \dhividhivya --password-stdin docker.io"
          sh 'docker push bharagy/pyimg'
        }
      }
    }
    
  }

post{
      always{
            sh 'docker rm -f mypycont'
            sh 'docker run --name mypycont -d -p 3000:5000 my-flask'
            mail to: "dhivineelakandan96@gmail.com",
            subject: "Notification mail from jenkins",
            body: "CiCd pipeline"
        }
}

}
    

  

