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

                    echo "Application: ${appName}"
                    echo "Version: ${appVersion}"

                    env.APP_NAME    = appName
                    env.APP_VERSION = appVersion
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh """
                        npm install
                    """
                }
        }
       
    post {
        always {
            echo "it will run always"
            // Optional: prune untagged/dangling images to save disk space on the agent
            //  docker push ${acc_id}.dkr.ecr.us-east-1.amazonaws.com/${project}/${component}:${appVersion}
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
}
}