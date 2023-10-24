pipeline {
    agent any

    stages {
        stage('Remove old files on Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.102.111'
                    
                    sshagent(['437bce8e-09d7-4292-b986-5364da9f7137']) {
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
                    
                sshagent(['437bce8e-09d7-4292-b986-5364da9f7137']) {
                        sh "scp -r ./* ${serverUser}@${serverHost}:${remotePath}"
                }
            }
        }
    }
}
}
