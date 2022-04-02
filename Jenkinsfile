pipeline {
    agent {
        docker { image 'node:16.13.1-alpine' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'git clone https://github.com/Eagle201700/TestFeathers.git'
                sh 'cd TestFeathers'
                sh 'npm install'
                sh 'node --version'
            }
        }
    }
}
