import groovy.json.JsonSlurperClassic

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
                    def packageJsonText = readFile 'package.json'
                    def packageJson     = new JsonSlurperClassic().parseText(packageJsonText)

                    env.APP_NAME    = packageJson.name
                    env.APP_VERSION = packageJson.version

                    echo "Application: ${env.APP_NAME}"
                    echo "Version: ${env.APP_VERSION}"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                echo "Building application: ${env.APP_NAME}..."
            }
        }
        stage('Test') {
            steps {
                echo 'Running unit tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying ${env.APP_NAME} to ${env.region}..."
            }
        }
    }
}