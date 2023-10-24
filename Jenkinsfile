pipeline {
    agent any

    stages {
        stage('Remove old files on Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.102.111'
                    
                    sshagent(['85b0bcf0-fdf1-4feb-8843-349a4fbe1058']) {
                        sh "ssh -v ${serverUser}@${serverHost} sudo rm -rf /var/www/html/*"
                    }
                }
            }
        }
        
        stage('Add new files to Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.102.111'
                    def remotePath = '/var/www/html/'
                    
                sshagent(['85b0bcf0-fdf1-4feb-8843-349a4fbe1058']) {
                        sh "scp -r ./* ${serverUser}@${serverHost}:${remotePath}"
                }
            }
        }
    }
}
}
