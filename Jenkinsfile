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
                    withCredentials([string(credentialsId: 'git-pat', variable: 'GIT_TOKEN')]) {
                        git branch: 'main', url: "https://${GIT_TOKEN}@github.com/seunayolu/pat_webserver.git"
                    }
                }
            }
        }
    }
}