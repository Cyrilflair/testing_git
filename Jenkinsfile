pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "<html><body><h1>Testing Hello, World!</h1></body></html>" > index.html'
            }
        }
        stage('Publish') {
            steps {
                archiveArtifacts artifacts: 'index.html'
            }
        }
    }
}
