pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/minyeokue/maven-webapp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn -DtestWelcome=TestWelcome'
            }
        }

        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-admin', url: 'http://192.168.56.102:8080')], contextPath: null, war: 'target/hello-world.war'
            }
        }
    }
}