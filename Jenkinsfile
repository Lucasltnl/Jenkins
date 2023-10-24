pipeline {
    agent any

    stages {
        stage('Remove old files on Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.102.111'
                    
                    sshagent(['675aea5d-b3f2-4b1b-9078-6401b41dc78f']) {
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
                    
                sshagent(['675aea5d-b3f2-4b1b-9078-6401b41dc78f']) {
                        sh "scp -r ./* ${serverUser}@${serverHost}:${remotePath}"
                }
            }
        }
    }
}
}
