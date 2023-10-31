pipeline {
    agent any

    stages {
        stage('Remove old files on Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.106.112'
                    // SSH-agent gebruiken voor de sleutel met de ID 'c314c421-76d7-4f9c-9e1f-8a14cc2e18eb'
                    def serverHost = '192.168.106.111'
                    
                    sshagent(['c314c421-76d7-4f9c-9e1f-8a14cc2e18eb']) {
                        sh "ssh -v ${serverUser}@${serverHost} sudo rm -rf /var/www/html/*"
                    }
                }
            }
        }
        
        stage('Add new files to Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.106.111'
                    def remotePath = '/var/www/html/'
                    
                sshagent(['c314c421-76d7-4f9c-9e1f-8a14cc2e18eb']) {
                        sh "scp -r ./* ${serverUser}@${serverHost}:${remotePath}"
                }
            }
        }
    }
}
}
