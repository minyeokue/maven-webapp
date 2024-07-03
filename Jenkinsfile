pipeline {
    agent {
        label "jenkins-node"
    }

    triggers {
        pollSCM 'H * * * *'
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
                sh 'mvn clean package -Dmaven.test.skip=true'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'tomcat-admin',
                        url: 'http://192.168.56.102:8080'
                        )
                ],
                contextPath: null,
                war: 'target/hello-world.war'
            }
        }
    }
}