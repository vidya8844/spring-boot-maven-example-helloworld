pipeline {
    agent any

    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
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
                sh 'java -jar  /var/lib/jenkins/workspace/spring-boot/target/SpringBootMavenExample-1.3.5.RELEASE.war'
            }
        }
    }
}
