pipeline {
    agent{
        label 'slave1'
    }
     tools {
        nodejs 'Node'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/aayyusssh/jenkins-nodejs-CI-CD-pipeline.git'
            }
        }

         stage('Build React App') {
            steps {
                dir('client') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Test React App') {
            steps {
                dir('client') {
                    sh 'CI=true npm test -- --coverage'
                }
            }
        }

        stage('Build Server') {
            steps {
                dir('server') {
                    sh 'npm install'
                }
            }
        }

        stage('Test Server') {
            steps {
                dir('server') {
                    sh 'npm test'
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'cp -R client/build/* server/build/'
            }
        }
    }

}
