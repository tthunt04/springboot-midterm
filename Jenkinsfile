pipeline {
    agent any

    environment {
        NEXUS_URL = 'http://localhost:8081/repository/maven-releases/'
        NEXUS_CREDENTIALS = 'nexus-cred'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-private-key',
                    url: 'git@github.com:tthunt04/springboot-midterm.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Upload to Nexus') {
            steps {
                script {
                    def jarFile = sh(script: "ls target/*.jar", returnStdout: true).trim()

                    withCredentials([usernamePassword(credentialsId: NEXUS_CREDENTIALS,
                        usernameVariable: 'USERNAME',
                        passwordVariable: 'PASSWORD')]) {

                        sh """
                        curl -v -u $USERNAME:$PASSWORD --upload-file $jarFile $NEXUS_URL
                        """
                    }
                }
            }
        }
    }
}
