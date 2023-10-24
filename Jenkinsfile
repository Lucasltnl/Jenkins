pipeline {
    agent any

    stages {
        stage('Remove old files on Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.138.112'
                    
                    sshagent(['b8b245b3-0567-4396-9267-e561f6d10e72']) {
                        sh "ssh -v ${serverUser}@${serverHost} sudo rm -rf /var/www/html/*"
                    }
                }
            }
        }
        
        stage('Add new files to Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.138.112'
                    def remotePath = '/var/www/html/'
                    
                sshagent(['b8b245b3-0567-4396-9267-e561f6d10e72']) {
                        sh "scp -r ./* ${serverUser}@${serverHost}:${remotePath}"
                }
            }
        }
    }
}
}
