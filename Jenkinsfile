pipeline{
    agent any
    stages{
        stage('checkout'){
            checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vamsi52002/raviLogin.git']])
        }
        stage('validate'){
            steps{
            sh 'mvn validate'
            }
        }
        stage('compile'){
            steps{
            sh 'mvn compile'
            }
        }
        stage('test'){
            steps{
            sh 'mvn test'
            }
        }  
        stage('package'){
            steps{
            sh 'mvn package'
            }
        }      

    }
}