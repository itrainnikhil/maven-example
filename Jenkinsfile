pipeline {
    agent any 
    stages {
        stage('Code Checkout') { 
            steps {
                sh 'echo code checkout'
                git credentialsId: 'githubID', url: 'https://github.com/itrain-org/maven-example.git'
            }
        }
        stage('Build') { 
            steps {
              withMaven(jdk: 'JDK-1.8', maven: 'Maven-3.6.1') {
               sh 'mvn clean compile'
             } 
            }
        }
        stage('Test') { 
            steps {
               withMaven(jdk: 'JDK-1.8', maven: 'Maven-3.6.1') {
               sh 'mvn test'
             }  
            }
        }
        
        stage('code analysis') { 
            steps {
                withMaven(jdk: 'JDK-1.8', maven: 'Maven-3.6.1') {
               sh 'mvn verify sonar:sonar \
                      -Dsonar.projectKey=maven-org-proj \
                      -Dsonar.organization=itrainnikhil \
                      -Dsonar.host.url=https://sonarcloud.io \
                      -Dsonar.login=f5ecb84e72d8184cdd2f5cc5167c667542600d53 '
             }  
            }
        }
        stage('Package') { 
            steps {
                withMaven(jdk: 'JDK-1.8', maven: 'Maven-3.6.1') {
               sh 'mvn package'
             }  
            }
        }
       
    }
}
