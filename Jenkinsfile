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

            post { 
                always { 
                    sh 'echo 13-Jenkinsfile Pipeline’da Test Raporu Script’i Yapilandirma-20/06/2024...'
                    junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'echo Deploying...'
                sh 'mvn package'
            }
        }
        
        stage('Build & Docker Image') {
            steps {
                sh 'echo Build & Docker Image...'
                sh 'docker build -t aysegulbulur/docker_jenkins_pipeline:${BUILD_NUMBER} .'
            }
        }
        
        stage('Docker login') {
            steps {
                sh 'echo Docker login...'
                withCredentials([string(credentialsId: 'DockerId', variable: 'Dockerpwd')]) {
		    sh 'docker login -u aysegulbulur -p ${Dockerpwd}'
		}
            }
        }
        
        stage('Push to Repository') {
            steps {
                sh 'echo Push to Repository...'
                sh 'docker push aysegulbulur/docker_jenkins_pipeline:${BUILD_NUMBER}'
            }
        }

        stage('Archving') {
            steps {
                sh 'echo Archving...'
                archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
