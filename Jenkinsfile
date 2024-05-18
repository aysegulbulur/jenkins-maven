pipeline {
    agent any
    stages {
        stage('Compile and Clean') {
            steps {
                sh 'echo Compile and Clean'
                sh 'mvn clean compile'
            }
        }
        
        stage('Test') {
            steps {
                sh 'echo Testing...'
                sh 'mvn test'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'echo Deploying...'
                sh 'mvn package'
            }
        }
    }
}
