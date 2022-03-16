pipeline{
    agent any
    tools { 
        maven 'Apache Maven 3.6.0'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'gittoken', url: 'https://github.com/Ray-Shubham/jenkins-docker-example.git']]])
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t 646504/my-app-1.0 .'
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                script {
                    withCredentials([string(credentialsId: '646504', variable: 'dockerpwd')]) {
                        sh 'docker login -u 646504 -p ${dockerpwd}'
}
                    sh 'docker push 646504/my-app-1.0'
                }
            }
        }
    }
    
}
