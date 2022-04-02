pipeline {
    agent{
            docker {
                image "node:16.13.1-alpine"
                args "-p 6379:6379"
            }
    }
    environment{
        CI="true"
        REDIS_HOST= "172.16.238.10"
    }
    stages{
        stage('Test') {
            steps {
                sh 'node --version'
            }
        }
        stage("Build"){
            steps{
                sh "npm install"
            }
        }
    }
    post{
        success{
            sh "node jenkins/scripts/publish_build.js"
        }
    }
}
