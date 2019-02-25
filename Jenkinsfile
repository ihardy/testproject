pipeline {
    agent { docker { image 'node:8-alpine' } }

    environment {
        TEST_VAR = 'a_test_env_var'
    }

    stages {
        stage('build') {
            steps {
                sh 'printenv'
                sh 'npm --version'
            }
        }
    }
}

