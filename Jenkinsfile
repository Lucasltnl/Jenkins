pipeline {
    agent any

    stages {
        stage('Remove old files on Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.102.112'
                    
                    sshagent(['1fa54fc2-dda9-4594-8c87-1d2e4a78c412']) {
                        sh "ssh -v ${serverUser}@${serverHost} sudo rm -rf /var/www/html/*"
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
                    
                sshagent(['1fa54fc2-dda9-4594-8c87-1d2e4a78c412']) {
                        sh "scp -r ./* ${serverUser}@${serverHost}:${remotePath}"
                }
            }
        }
    }
}
}
