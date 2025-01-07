 pipeline {     
    agent {label 'slave-1'} 
    
    tools {
        maven 'Maven'
        jdk 'JDK17'
    }

    stages {

        stage('Compile') {
            steps {
            sh  "mvn compile"
            }
        }
        
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }
        
        stage('Build') {
            steps {
                sh "mvn package"
            }
        }
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'Tomcat-Credentials', path: '', url: 'http://13.233.25.147:8080/')], contextPath: 'fullstack', onFailure: false, war: 'target/*.war'
            }
        }
    }
}
