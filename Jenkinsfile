def withDockerNetwork(Closure inner) {
  try {
    networkId = UUID.randomUUID().toString()
    sh "docker network create ${networkId}"
    inner.call(networkId)
  } finally {
    sh "docker network rm ${networkId}"
  }
}

pipeline {
    agent none
    environment{
        CI="true"
        REDIS_HOST= "172.16.238.10"
    }
    stages {
        stage('Back-end') {
            agent{
                docker {
                    image "node:16.13.1-alpine"
                    args "-p 6379:6379"
                }
            }
            steps {
                sh 'node --version'
                sh "npm install"
                sh "docker run -d -p 27017:27017 --name example-mongo mongo:latest "
            }
        }
        stage('Front-end') {
            agent {
                docker { image 'node:16.13.1-alpine' }
            }
            steps {
                sh 'node --version'
            }
        }
    }
//     agent{
//         docker {
//             image "node:16.13.1-alpine"
//             args "-p 6379:6379"
//         }
//     }
//     stages{
//         stage('Test') {
//             steps {
//                 sh 'node --version'
//             }
//         }
//         stage("Build"){
//             steps{
//                 sh "npm install"
//             }
//         }
//     }
    post{
        success{
            sh "node jenkins/scripts/publish_build.js"
        }
    }
}
