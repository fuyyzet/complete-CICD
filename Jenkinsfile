pipeline {
  agent any
  tools {
    maven "maven3"
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