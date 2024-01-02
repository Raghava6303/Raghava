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
        stage('deploying-APP'){
            steps{
               deploy adapters: [tomcat9(credentialsId: 't-dev', path: '', url: 'http://3.85.33.37:8080/')], contextPath: 't-dev', war: '**/*.war'
            }
        }
        stage('Test ENV'){
            steps{
                script {
                    def A = input (
                        message: 'do you want to deploy in developer',
                        id: 't-dev',
                        ok: 'YES',
                        submitter: 'YES'
                    )
                    if(A == 'YES') {
                        deploy adapters: [tomcat9(credentialsId: 't-dev', path: '', url: 'http://34.239.144.208:8080/')], contextPath: 't-test', war: '**/*.war'
                    }
                    else{
                        echo ("ABORT")
                    }
                }
            }
        }
        stage('PRE-PROD ENV'){
            steps{
                script {
                    def B = input (
                        message: 'do you want to deploy in developer',
                        id: 't-dev',
                        ok: 'YES',
                        submitter: 'YES'
                    )
                    if(B == 'YES') {
                        deploy adapters: [tomcat9(credentialsId: 't-dev', path: '', url: 'http://18.232.142.107:8080/')], contextPath: 't-test', war: '**/*.war'
                    }
                    else{
                        echo ("ABORT")
                    }
                }
            }
        }
        stage('PROD ENV'){
            steps{
                script {
                    def A = input (
                        message: 'do you want to deploy in developer',
                        id: 't-dev',
                        ok: 'YES',
                        submitter: 'YES'
                    )
                    if(A == 'YES') {
                        deploy adapters: [tomcat9(credentialsId: 't-dev', path: '', url: 'http://18.206.186.233:8080/')], contextPath: 't-test', war: '**/*.war'
                    }
                    else{
                        echo ("ABORT")
                    }
                }
            }
        }
    }
}

