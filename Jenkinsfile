pipeline {
    agent any
    environment {
        SONARQUBE_TOKEN = credentials('sonarqube-token')  // Remplace par l'identifiant du token dans Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                // Récupère le code depuis le dépôt GitHub
                git url: 'https://github.com/tonnomutilisateur/tondepot.git', branch: 'main'
            }
        }
        stage('Install Node.js') {
            steps {
                // Installe la version Node.js requise
                nodejs('NodeJS 14')  // Assure-toi que cette version est configurée dans Jenkins
            }
        }
        stage('Install Dependencies') {
            steps {
                // Installe les dépendances du projet Node.js
                sh 'npm install'
            }
        }
        stage('Run SonarQube Analysis') {
            steps {
                script {
                    // Exécute l'analyse SonarQube
                    sh """
                        sonar-scanner \
                            -Dsonar.projectKey=pr_sonar \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.login=${SONARQUBE_TOKEN}
                    """
                }
            }
        }
    }
}
