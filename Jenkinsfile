pipeline {
    agent any

    stages {
        stage('Checkout from Git') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: 'dev']],
                        userRemoteConfigs: [[url: 'https://github.com/Lucasltnl/Jenkins.git']]
                    ])
                }
            }
        }

        stage('Remove old files on Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.106.112'

                    // SSH-agent gebruiken voor de sleutel met de ID 'c314c421-76d7-4f9c-9e1f-8a14cc2e18eb'
                    sshagent(['c314c421-76d7-4f9c-9e1f-8a14cc2e18eb']) {
                        // Voeg debugging-uitvoer toe
                        echo "Removing old files on Ubuntu"
                        sh "ssh -v ${serverUser}@${serverHost} sudo rm -rf /var/www/html/* 2>&1"
                    }
                }
            }
        }

        stage('Add new files to Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.106.112'
                    def remotePath = '/var/www/html/'

                    // SSH-agent gebruiken voor dezelfde sleutel
                    sshagent(['c314c421-76d7-4f9c-9e1f-8a14cc2e18eb']) {
                        // Voeg debugging-uitvoer toe
                        echo "Adding new files to Ubuntu"
                        sh "scp -r ./* ${serverUser}@${serverHost}:${remotePath} 2>&1"
                    }
                }
            }
        }
    }
}
