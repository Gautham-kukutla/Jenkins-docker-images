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
              withCredentials([usernamePassword(credentialsId: 'dockerup', passwordVariable: 'dockerpwd', usernameVariable: 'dockerusrn')]) {
                  sh "docker build -t gauthamkukutla/myrepo1 ."
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerup', passwordVariable: 'dockerpwd', usernameVariable: 'dockerusrn')]) {
                        sh "docker login -u ${dockerusrn} -p ${dockerpwd}"
}
                    sh "docker push ${dockerusrn}/myrepo1"
                }
            }
        }
    }
    
}
