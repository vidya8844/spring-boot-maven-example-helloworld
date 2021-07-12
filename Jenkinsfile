pipeline {
    agent any

    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
                sh 'mv */target/*.war target/myweb.war'
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
                sh 'java -jar target/myweb.war'
            }
        }
        stage('Sanity') {
            steps {
                sh 'curl -X GET http://65.1.65.1:8090/index.html'
            }
        }
    }
}
