pipeline {
    agent any

    stages {
        stage('Remove old files on Ubuntu') {
            steps {
                script {
                    def serverUser = 'student'
                    def serverHost = '192.168.102.112'
                    
                    try {
                        sshagent(['1fa54fc2-dda9-4594-8c87-1d2e4a78c412']) {
                            sh "ssh -v ${serverUser}@${serverHost} sudo rm -rf /var/www/html/*"
                        }
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        echo "Fout bij het verwijderen van oude bestanden: ${e}"
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
                    
                    try {
                        sshagent(['1fa54fc2-dda9-4594-8c87-1d2e4a78c412']) {
                            sh "scp -r ./* ${serverUser}@${serverHost}:${remotePath}"
                        }
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        echo "Fout bij het toevoegen van nieuwe bestanden: ${e}"
                    }
                }
            }
        }
    }
}
