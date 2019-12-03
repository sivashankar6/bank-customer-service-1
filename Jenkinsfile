pipeline {
  agent any
  tools { 
        maven 'Maven3'
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
        sh '/usr/bin/docker build -t premvallab/bank-customer-service:latest .'
      }
    }
    stage('Push image') {
      steps {
        withDockerRegistry([credentialsId: 'premvallab', url: "https://index.docker.io/v1/"]) {
        //withDockerRegistry(credentialsId: 'premvallab, url: 'http://651843681614.dkr.ecr.ap-south-1.amazonaws.com/myrepo') {
          sh '/usr/bin/docker tag premvallab/bank-customer-service:latest'
          sh '/usr/bin/docker push premvallab/bank-customer-service:latest'
         //withDockerRegistry(credentialsId: 'premvallab:mycredentials', url: "https://index.docker.io/v2/"] {
          //sh 'docker tag premvallab/bank-customer-service:latest 651843681614.dkr.ecr.ap-south-1.amazonaws.com/myrepo:latest'
          //sh 'docker push 651843681614.dkr.ecr.ap-south-1.amazonaws.com/myrepo:latest'
        }
      }
    }
  }
}
