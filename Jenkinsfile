pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/errachidy10/test_repo.git'
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean package' // Utilisez 'bat' au lieu de 'sh' pour Windows
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat 'mvn sonar:sonar' // Utilisez 'bat' au lieu de 'sh' pour Windows
                }
            }
        }
    }
}
