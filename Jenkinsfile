pipeline {
  agent any
  environment {
    		DOCKERHUB_CREDENTIALS=credentials('dh_cred')
  }
  stages {
    stage('login to DH'){
      steps{
          sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('app') {
           when {
        changeset "**/app/*.*"
        beforeAgent true
      }
        steps {
          sh 'docker build -t epsdevops/app -f packages/app/Dockerfile packages/app'
          sh 'docker push epsdevops/app'
      }
    }
    stage('components') {
           when {
        changeset "**/components/*.*"
        beforeAgent true
      }
      steps {
          sh 'docker build -t epsdevops/components -f packages/components/Dockerfile packages/components'
          sh 'docker push epsdevops/components'
      }
    }
    stage('server') {
             when {
        changeset "**/server/*.*"
        beforeAgent true
      }
      steps {
       
          sh 'docker build -t epsdevops/server -f packages/server/Dockerfile packages/server'
          sh 'docker push epsdevops/server'
      }
    }
    stage('clean') {
      steps {
          sh 'docker image prune -a -f'
          sh 'docker container prune -f'        
      }
    }
    }
  }
