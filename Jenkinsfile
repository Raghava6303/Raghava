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
               deploy adapters: [tomcat9(credentialsId: 'jt', path: '', url: 'http://54.91.6.45:8080/')], contextPath: 'jai', war: '**/*.war'
            }
        }
        parameters {
            choice choices: ['True'], description: 'deploy to tomcat test', name: 'tomcat test'
        }
        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp -i Desktop/main.pem **/*.war jenkins@${params.tomcat_stage}:/usr/share/apache-tomcat-9.0.84/webapps/"
                    }
                }
                stage ("Deploy to Production"){
                    steps {
                        sh "scp **/*.war jenkins@${params.tomcat_prod}:/usr/share/apache-tomcat-9.0.84/webapps/"
                    }
                }
            }
        }
    }
}
