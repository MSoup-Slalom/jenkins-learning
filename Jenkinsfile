/* Requires the Docker Pipeline plugin */
pipeline {
    agent { docker { image 'node:18.16.0-alpine' } }
    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE = 'sqlite'
    }
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello World"'
                sh 'node --version'
                sh '''
                    echo "Multiline shell step"
                    ls -lah
                '''
                
                // timeout(time: 3, unit: 'MINUTES') {
                //     retry(3) {
                //         sh './flakey-deploy.sh'
                //     }
                // }
            }
        }
        stage('access_env') {
            steps {
                echo "Database engine is ${DB_ENGINE}"
                echo "DISABLE_AUTH is ${DISABLE_AUTH}"
                sh 'printenv' 
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
