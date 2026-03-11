/* Requires the Docker Pipeline plugin */
pipeline {
    agent { docker { image 'python:3.14.3-alpine3.23' } }

    environment {   
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }

    stages {
        stage('verify') {
            steps {
                echo "Database engine is ${DB_ENGINE}"
                echo "DISABLE_AUTH is ${DISABLE_AUTH}"
                sh 'printenv'
            }
        }
        stage('build') {
            steps {
                sh 'python --version'
            }
        }
        stage('test') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        stage('deploy-staging') {
            steps {
                echo "Deploying to staging."
                echo "Staging deployed."
            }
        }
        stage('approval') {
            steps {
                input "Does the staging environment look ok?"
            }
        }
        stage('deploy-prod') {
            steps {
                echo "Deploying to production."
                echo "Production deployed."
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}