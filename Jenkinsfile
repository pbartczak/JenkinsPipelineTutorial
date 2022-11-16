pipeline {
    agent any

    stages {
        stage("build") {
            steps {
                echo "building the application...."
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
