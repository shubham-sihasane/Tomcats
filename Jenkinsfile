 pipeline {     
    agent any
    
    tools {
        maven 'Maven'
        jdk 'JDK17'
    }

    parameters {
        // string (name: 'Branch_Name', defaultValue: main, description: 'Select the branch name:')
        choice (name: 'Branch_Name', choices: ['main','dev','test'], description: 'Select the branch name:')
    }
    
    stages {
        
        stage('Git Checkout') {
            steps {
                git branch: "${params.branch_Name}", url: 'https://github.com/shubham-sihasane/Tomcats.git'
            }
        }
         
        stage('Compile') {
            steps {
                sh  "mvn compile"
            }
        }
        
        stage('tests') {
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
