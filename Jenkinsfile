pipeline {
    agent any

    stages {
        stage('Remove old files on Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.102.112'
                    def remotePath = '/var/www/html/'

                    sshagent(credentials: ['1fa54fc2-dda9-4594-8c87-1d2e4a78c412']) {
                        // SSH-oproep met debuglogboek
                        sh "ssh -v ${serverUser}@${serverHost} sudo rm -rf ${remotePath}* 2>&1"
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

                    sshagent(credentials: ['1fa54fc2-dda9-4594-8c87-1d2e4a78c412']) {
                        // SCP-oproep met debuglogboek
                        sh "scp -rv ./* ${serverUser}@${serverHost}:${remotePath} 2>&1"
                    }
                }
            }
        }
    }
}
