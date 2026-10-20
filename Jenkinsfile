pipeline {
    agent {
        docker {
            image 'maven:3.9.6-eclipse-temurin-17'
            args '-v $HOME/.m2:/root/.m2'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Private Deploy') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'nexus-deployment-creds',
                    usernameVariable: 'NEXUS_USERNAME',
                    passwordVariable: 'NEXUS_PASSWORD'
                )]) {
                    sh 'mvn clean deploy -s maven-settings.xml'
                }
            }
        }
    }
}
