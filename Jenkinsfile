pipeline {
    agent any
    tools{
        maven 'maven_3_5_0'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/bangga0403/devops-automation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t bangga0403/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'bangga0403', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u bangga0403 -p ${dockerhubpwd}'

                    }
                   sh 'docker push bangga0403/devops-integration'
                }
            }
        }
    }
}