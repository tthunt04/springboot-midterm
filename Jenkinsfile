stage('Upload to Nexus') {
    steps {
        script {
            def jarFile = sh(script: "ls target/*.jar", returnStdout: true).trim()

            withCredentials([usernamePassword(credentialsId: 'nexus-cred',
                usernameVariable: 'USERNAME',
                passwordVariable: 'PASSWORD')]) {

                sh """
                curl -v -u $USERNAME:$PASSWORD --upload-file $jarFile http://localhost:8081/repository/maven-releases/
                """
            }
        }
    }
}
