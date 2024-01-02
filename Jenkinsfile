pipeline{
    agent any
    stages{
        stage('checkout'){
            steps{
            checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Raghava6303/raviLogin.git']])
            }
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
        stage('deploy to tomcat'){
            steps{
               deploy adapters: [tomcat9(credentialsId: 't-dev', path: '', url: 'http://3.85.33.37:8080/')], contextPath: 't-dev', war: '**/*.war'
            }
        }
    }
}
