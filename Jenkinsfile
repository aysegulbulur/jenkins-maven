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
        
        stage('Build Docker image') {
            steps {
                sh 'echo Build Docker image...'
                sh 'docker build -t aysegulbulur/docker_jenkins_pipeline:${BUILD_NUMBER} .'
            }
        }
        
        stage('Docker Login') {
            steps {
                sh 'echo Docker Login...'
                withCredentials([string(credentialsId: 'DockerId', variable: 'Dockerpwd')]) {
		    sh 'docker login -u aysegulbulur -p ${Dockerpwd}'
		}
            }
        }
        
        stage('Docker Push') {
            steps {
                sh 'echo Docker Push...'
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
