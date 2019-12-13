pipeline {
   
   agent any 
   tools {
    maven 'Apache Maven 3.6.2'
  }
 
    stages {
       
       stage('Checkout'){
          steps{
          sh 'rm -rf Maven-Project'
          sh 'git clone https://github.com/VivekRaveendrn/Maven-Project.git'
          }
       }
       
       
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
       
       stage('Sonarqube') {
   
 steps {
        script {
          // requires SonarQube Scanner 2.8+
          scannerHome = tool 'SonarQube'
        }
        withSonarQubeEnv('SonarQube') {
          sh "${scannerHome}/bin/sonar-scanner"
        }
      }
       }
       
       
       stage('build and push docker image') {
    steps {
    // Using Google JIB plugin                                                                                                         
    sh 'mvn compile com.google.cloud.tools:jib-maven-plugin:1.3.0:build'
    }
}
       
       
      
    }
}
