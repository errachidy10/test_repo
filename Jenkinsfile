pipeline {
    agent any

    tools {
        // Assurez-vous d'avoir configuré JDK 21 dans Jenkins
        maven 'mvn'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
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
