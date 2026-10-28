pipeline {
    agent any

    stages {
        stage('Build and Test') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }
}
