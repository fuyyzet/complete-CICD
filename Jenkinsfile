  pipeline {
  agent any
  // {
    //docker {
    //  image 'maven:3.8.4-openjdk-17'
     // args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
   // }
  //}
  //environment {
   // DOCKERHUB_CREDENTIALS = credentials('Eyere-dockerhub')
   // APP_NAME = "fuzzyet/amazon-clone"
   // }
  stages {
    stage('Checkout') {
      steps {
        sh 'echo passed'
        //git branch: 'main', url: 'https://github.com/iam-veeramalla/Jenkins-Zero-To-Hero.git'
      }
    }
    stage('Build and Test') {
      steps {
        //sh 'ls -ltr'
        // build the project and create a JAR file
        sh 'cd spring && mvn clean package' 
      }
    }
    stage('Static Code Analysis') {
      environment {
        SONAR_URL = "http://18.206.207.126:9000"
      }
      steps {
        withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_AUTH_TOKEN')]) {
          sh 'cd spring && mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
        }
      }
    }
    stage('Build and Push Docker Image') {
      environment {
        DOCKER_IMAGE = "fuzzyet/complete-cicd:${BUILD_NUMBER}"
        REGISTRY_CREDENTIALS = credentials('docker-cred')
      }
      steps {
        script {
            sh 'cd spring && docker build -t ${DOCKER_IMAGE} .'
            sh 'echo ${REGISTRY_CREDENTIALS}'
            def dockerImage = docker.image("${DOCKER_IMAGE}")
            docker.withRegistry('https://index.docker.io/v1/', "docker-cred") {
                dockerImage.push()
            }
        }
      }
    }
    
  }
}