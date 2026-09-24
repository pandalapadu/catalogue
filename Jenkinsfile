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
    stages {
        stage('Read Version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'

                    def appName    = packageJson.name
                    def appVersion = packageJson.version

                    echo "Application: ${appName}"
                    echo "Version: ${appVersion}"

                    env.APP_NAME    = appName
                    env.APP_VERSION = appVersion
                }
            }
        }
        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running unit tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying artifact...'
            }
        }
    }
}