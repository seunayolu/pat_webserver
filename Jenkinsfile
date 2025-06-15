pipeline {
    agent {
        label 'node-01'
    }

    environment {
        Instance_IP = '172.31.38.21'
        ServerName = 'ubuntu'
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

        stage ('deploytoec2') {
            steps {
                script {
                    echo "Deploy a shell script to Amazon EC2 Instance"
                    def shellscript = "bash ./websetup.sh"
                    sshagent(['sshkey']) {
                        sh "scp -o StrictHostKeyChecking=no websetup.sh ${ServerName}@${Instance_IP}:/home/ubuntu"
                        sh "ssh -o StrictHostKeyChecking=no ${ServerName}@${Instance_IP} ${shellscript}"
                    }
                }
            }
        }
    }
}