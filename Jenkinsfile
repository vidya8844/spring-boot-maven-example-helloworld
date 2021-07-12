pipeline {
    agent any

    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                sh 'pkill -f \'java -jar\''
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
                withEnv(['JENKINS_NODE_COOKIE=dontkill']) {
                    sh 'nohup mvn spring-boot:run -Dserver.port=8090 &'
                }
            }
        }
        stage('Sanity') {
            steps {
                echo 'Waiting to boot up application'.
                sh 'sleep 30s'
                sh 'curl -X GET http://65.1.65.1:8090/index.html'
            }
        }
    }
}
