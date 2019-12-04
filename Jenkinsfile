pipeline {
  agent any
  tools { 
        //maven 'Maven3'
        jdk 'jdk'
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
        sh '/usr/bin/docker build -t sivashankar6/bank-customer-service:latest .'
      }
    }
    stage('Push image') {
      steps {
        withDockerRegistry([credentialsId: 'adapachoshi', url: "https://index.docker.io/v1/"]) {
        //withDockerRegistry(credentialsId: 'sivashankar6', url: 'https://118463809662.dkr.ecr.ap-south-1.amazonaws.com/sivashankar6') {
          sh '/usr/bin/docker tag 9aea46245759 adapachoshi/bank-customer-service:latest'
          sh '/usr/bin/docker push adapachoshi/bank-customer-service:latest'
         //withDockerRegistry(credentialsId: 'ecr:ap-south-1:mycredentials', url: 'http://118463809662.dkr.ecr.ap-south-1.amazonaws.com/myrepo') {
          //sh 'docker tag sivashankar6/bank-customer-service:latest 118463809662.dkr.ecr.ap-south-1.amazonaws.com/myrepo:v2'
          //sh 'docker push 118463809662.dkr.ecr.ap-south-1.amazonaws.com/myrepo:v2'
        }
      }
    }
  }
}
