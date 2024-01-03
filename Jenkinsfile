pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages {
        stage("Build Artifact") {
            steps {
                script {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }
        stage("Test") {
            steps {
                script {
                    sh 'mvn test'
                }
            }
        }
        stage('Deploy') {
        steps {
            sshagent(credentials: ['301sudheer']) {
                
                sh "ssh ubuntu@100.25.35.77 'sudo mv ~/vprofile-v1.war /var/lib/tomcat9/webapps/'"
                sh "ssh ubuntu@100.25.35.77 'sudo systemctl restart tomcat9'"
            }
        }
    }
    }
}
