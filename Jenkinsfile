pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package' // build the WAR file using Maven
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'tomcat', usernameVariable: 'admin', passwordVariable: 'admin')]) {
                    // deploy the WAR file to Tomcat using curl
                    sh 'curl -u $TOMCAT_USER:$TOMCAT_PASS -T target/hello-world.war http://13.250.64.185:8080/manager/text/deploy?path=/hello-world&update=true'
                }
            }
        }
    }

    post {
        always {
            // cleanup after the build by undeploying the app from Tomcat
            withCredentials([usernamePassword(credentialsId: 'tomcat', usernameVariable: 'admin', passwordVariable: 'admin')]) {
                sh 'curl -u $TOMCAT_USER:$TOMCAT_PASS http://13.250.64.185:8080/manager/text/undeploy?path=/hello-world'
            }
        }
    }
}
