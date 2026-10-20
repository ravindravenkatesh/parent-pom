pipeline {
    agent any

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
