pipeline {
    agent {
        node {
            label 'ROBOSHOP'
        }
    }

    environment {
        acc_id    = "453388807064"
        project   = "roboshop"
        component = "catalogue"
        region    = "us-east-1"
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 15, unit: 'MINUTES')
    }

    stages {
        stage('Read Version') {
            steps {
                script {
                    // Uses Node.js CLI to parse package.json (avoids missing plugin & sandbox approval errors)
                    env.APP_NAME    = sh(script: "node -p \"require('./package.json').name\"", returnStdout: true).trim()
                    env.APP_VERSION = sh(script: "node -p \"require('./package.json').version\"", returnStdout: true).trim()

                    echo "Application: ${env.APP_NAME}"
                    echo "Version: ${env.APP_VERSION}"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh """
                    npm install
                """
            }
        }
    }

    post {
        always {
            echo "it will run always"
            sh 'docker image prune -f'
        }
        success {
            echo "I will run only success"
        }
        failure {
            echo "I will run if build failed"
        }
    }
}