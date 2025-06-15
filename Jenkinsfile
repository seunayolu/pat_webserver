pipeline {
    agent {
        label 'node-01'
    }

    environment {
        Instance_IP = '172.31.38.21'
    }

    stages {
        stage ('fetch_code') {
            steps {
                script {
                    echo "Pulling source code from GitHub"
                    git branch: 'main', url: 'git@github.com:seunayolu/pat_webserver.git'
                }
            }
        }
    }
}