pipeline {
    agent any

    tools {
        // Assurez-vous d'avoir configuré JDK 21 dans Jenkins
        maven 'mvn'
    }

    environment {
        MAVEN_OPTS = '-Dmaven.wagon.http.ssl.insecure=true -Dmaven.wagon.http.ssl.allowall=true'
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat 'mvn sonar:sonar'
                }
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
