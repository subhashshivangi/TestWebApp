pipeline {

    agent any

    tools {
        maven 'Maven'
    }

    environment {
        TOMCAT_URL = 'http://3.26.204.115:9090/'
        APP_NAME = 'maven-web-app'
    }

    stages {

        stage('Get Code') {
            steps {
                git 'https://github.com/subhashshivangi/TestWebApp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy to Tomcat') {
            steps {

                withCredentials([
                    usernamePassword(
                        credentialsId: 'tomcat-credentials',
                        usernameVariable: 'admin',
                        passwordVariable: 'Admin@123'
                    )
                ]) {

                    sh '''
                        curl --fail --upload-file target/TestWebApp.war \
                        -u "admin:Admin@123" \
                        "http://3.26.204.115:9090/manager/text/deploy?path=/TestWebApp&update=true"
                    '''
                }
            }
        }
    }
}
