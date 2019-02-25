pipeline {
    agent { docker { image 'node:8' } }
    stages {
        stage('build') {
            steps {
                sh 'echo "multistep test"'
                sh 'npm --version'
            }
        }
    }
}

