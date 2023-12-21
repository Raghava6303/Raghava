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
               deploy adapters: [tomcat9(credentialsId: 'tj', path: '', url: 'http://54.91.6.45:8080/')], contextPath: 'jai', war: '**/*.war'
            }
        }
    }
}
