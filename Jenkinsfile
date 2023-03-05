pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                tomcat deployUrl: 'http://13.250.64.185:8080/manager/text', credentialsId: 'tomcat', war: 'target/*.war'
            }
        }
    }
}
