pipeline {
    agent any
    environment {
        NEW_VERSION = "1.3.0"
        SERVER_CREDENTIALS = credentials('server-credentials')
    }
    stages {
        stage("build") {
            steps {
                echo "building the application...."
                echo "building version ${NEW_VERSION}"
                echo "credentials:  $SERVER_CREDENTIALS_PSW"
            }
        }
        stage("test") {
            when {
                expression {
                    env.BRANCH_NAME == 'dev' || env.BRANCH_NAME == 'test'
                }
            }
            steps {
                echo "testing the application...."
            }
        }
        stage("deploy") {
            steps {
                echo "deploying the applications...."
                withCredentials([usernamePassword(credentialsId: 'server-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'echo $USERNAME $PASSWORD'
                }
            }
        }
    }
    post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() // clean up our workspace
        }
        success {
            echo "I succeeded!"
        }
        unstable {
            echo "I am unstable :/"
        }
        failure {
            echo "I failed :("
        }
        changed {
            echo "Things were different before..."
        }
    }
}
