pipeline {
    agent any

    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                sh 'sleep 3'
                sh 'mvn clean package'
                sh 'echo build sucess'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                withEnv(['JENKINS_NODE_COOKIE=dontkill']) {
                    sh 'nohup mvn spring-boot:run -Dserver.port=8090 &'
                }
            }
        }
        stage('Sanity') {
            steps {
                sh 'sleep 15'
                sh 'curl -X GET http://65.1.65.1:8090/index.html'
            }
        }
    }
}
