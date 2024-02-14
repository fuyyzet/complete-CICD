  pipeline {
  agent {
    docker {
      image 'maven:3.8.4-openjdk-17'
      args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
    }
  }
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
    
        
    
  }
}