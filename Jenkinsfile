pipeline {
  agent any
  tools { 
        maven 'Maven'
        jdk 'JAVA_HOME'
  }
  stages {
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace... */
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        sh 'echo $USER'
        sh 'echo whoami'
      }
    }
    stage('Docker Build') {
      steps {
        sh '/usr/bin/docker build -t dvisanand/bank-customer-service:latest .'
      }
    }
    stage('Push image') {
      steps {
        //withDockerRegistry([credentialsId: 'dvisanand', url: "https://index.docker.io/v1/"]) {
        withDockerRegistry(credentialsId: 'dvishalanand', url: 'https://118463809662.dkr.ecr.ap-south-1.amazonaws.com/visanand') {
          sh '/usr/bin/docker push dvisanand/bank-customer-service:latest'
        }
      }
    }
  }
}
