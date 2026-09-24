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
                    def packageJson = readJSON file: 'package.json'
                    def appName    = packageJson.name
                    def appVersion = packageJson.version

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