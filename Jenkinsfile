pipeline {
    agent any

    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
                //sh 'mv /var/lib/jenkins/workspace/spring-boot/target/SpringBootMavenExample-1.3.5.RELEASE.war target/myweb.war'
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
                sh 'nohup mvn spring-boot:run'
            }
        }
        stage('Sanity') {
            steps {
                sh 'curl -X GET http://65.1.65.1:8090/index.html'
            }
        }
    }
}
