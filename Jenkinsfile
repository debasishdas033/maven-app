pipeline {
    agent any

    stages {
        stage('Clean the workspace') {
            steps {
                cleanWs()
            }
            
        }
        stage('Code Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'a0a92755-710d-4e73-9ab6-a7a976eb99ad', url: 'https://github.com/debasishdas033/maven-app.git']]])
                }
        }
        stage('Code Build') {
            steps {
                bat 'cd %WORKSPACE%'
                bat 'mkdir target'
                bat 'mvn package'
        }
        }
        stage('Code Deployment') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '9426b82f-9345-45df-9d5b-e0ae76960ee5', path: '', url: 'http://localhost:8080')], contextPath: 'SpringMVC4', onFailure: false, war: 'target/SpringMVC4.war'
            }
        }
                
    }
}
