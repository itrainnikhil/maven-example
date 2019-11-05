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
               sh 'mvn sonar:sonar \
                    -Dsonar.projectKey=maven-example-org \
                    -Dsonar.organization=itrain-org \
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.login=0d224e403d4845b132586bf6493149ffd760df78'
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
