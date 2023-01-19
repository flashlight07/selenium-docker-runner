pipeline {
    // master executor should be set to 0
    agent any
    stages {
        stage('Pull latest image') {
            steps {
                bat "docker pull ssomanpfpt/selenium-docker"
            }
        }
		stage('Bring grid up') {
            steps {
                bat "docker-compose up -d hub chrome firefox"
            }
        }
        stage('Run Tests') {
            steps {
                bat "docker-compose up search-module1 search-module2 book-flight-module1 book-flight-module2"
            }
        }
    }
	post {
		always {
			archiveArtifacts artifacts: 'output/**'
			bat "docker-compose down"
		}
	}
}