pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git branch:'main', credentialsId: '11', url: 'https://github.com/Ma-Zava11/Devops.git'
            }
        }

        stage('Build the application') {
            steps {
                bat 'mvn clean install'
            }
        }
         stage('UnitTestExecution'){
             steps{
                bat 'mvn test'
             }
        }
         stage('Build the docker image'){
             steps{
                bat 'docker build -t mazava/repostp2:1.0.0 .'
             }
        }
        stage('Push the docker image') {
             steps {
                withCredentials([usernamePassword(credentialsId: '29', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                bat 'docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%'
            }
                bat 'docker push mazava/repostp2:1.0.0'
            }
        }
    }
}
