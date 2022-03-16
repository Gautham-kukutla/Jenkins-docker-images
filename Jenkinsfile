pipeline{
    agent any
    tools { 
        maven 'Apache Maven 3.6.3'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'gittoken', url: 'https://github.com/Gautham-kukutla/jenkins-docker-example.git']]])
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

            }
        }
        stage('Build Docker Image') {
            steps {
                  sh 'docker build -t gauthamkukutla/myrepo1 .'
                }
            }
        stage('Deploy Docker Image') {
            steps {
                script {
                   withCredentials([string(credentialsId: 'dockersec', variable: 'dockerpwd')]) {
                        sh "docker login -u gauthamkukutla -p ${dockerpwd}"
}
                    sh 'docker push gauthamkukutla/myrepo1'
                }
            }
        }
    }
    
}
