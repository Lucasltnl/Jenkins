pipeline {
    agent any

    stages {
        stage('Checkout from Git') {
            steps {
                // Git-plugin om de GitHub-repo te klonen
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: 'dev']], // De gewenste branch is 'dev'
                        userRemoteConfigs: [[url: 'https://github.com/Lucasltnl/Jenkins.git']] // GitHub-repo URL
                    ])
                }
            }
        }
        
        stage('Remove old files on Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.102.112'
                    
                    // Verwijder de oude bestanden op de doelserver
                    sh "ssh -v ${serverUser}@${serverHost} sudo rm -rf /var/www/html/* 2>&1"
                }
            }
        }
        
        stage('Add new files to Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.102.112'
                    def remotePath = '/var/www/html/'
                    
                    // Kopieer bestanden van de Jenkins-workspace naar de doelserver
                    sh "scp -r ./* ${serverUser}@${serverHost}:${remotePath} 2>&1"
                }
            }
        }
    }
}
