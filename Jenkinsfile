pipeline {
  agent any
  tools { 
        maven 'Maven3'
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
        //sh '/usr/bin/docker build -t bank-customer-service .'
        sh '/usr/bin/docker build -t myrepo .'
      }
    }
    stage('Push image') {
      steps {
        //withDockerRegistry([credentialsId: 'premvallab', url: "https://index.docker.io/v1/"]) {
        //withDockerRegistry(credentialsId: 'premvallab, url: 'http://651843681614.dkr.ecr.ap-south-1.amazonaws.com/myrepo') {
          //sh '/usr/bin/docker tag bank-customer-service premvallab/firstrepo:latest'
          //sh '/usr/bin/docker push premvallab/firstrepo:latest'
         withDockerRegistry(credentialsId: 'ecr:us-east-1:docker', url: "750735215122.dkr.ecr.us-east-1.amazonaws.com/myrepo:latest") {
          sh 'docker tag myrepo:latest 750735215122.dkr.ecr.us-east-1.amazonaws.com/myrepo:latest'
          sh 'docker push 750735215122.dkr.ecr.us-east-1.amazonaws.com/myrepo:latest'
         }
        }
      }
    }
   }
  

