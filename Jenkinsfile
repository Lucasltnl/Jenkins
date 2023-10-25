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
                    def serverHost = '192.168.102.112'

                    // SSH-agent gebruiken voor de sleutel met de ID '1fa54fc2-dda9-4594-8c87-1d2e4a78c412'
                    sshagent(['437bce8e-09d7-4292-b986-5364da9f7137']) {
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
                    def serverHost = '192.168.102.112'
                    def remotePath = '/var/www/html/'

                    // SSH-agent gebruiken voor dezelfde sleutel
                    sshagent(['437bce8e-09d7-4292-b986-5364da9f7137']) {
                        // Voeg debugging-uitvoer toe
                        echo "Adding new files to Ubuntu"
                        sh "scp -r ./* ${serverUser}@${serverHost}:${remotePath} 2>&1"
                    }
                }
            }
        }
    }
}
