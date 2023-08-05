pipeline {
    agent any
    environment {
        staging_server = "12.7.108.141"
        staging_port = 8081
        ssh_username = "devops"
        ssh_password = "Pelatihan99!"
    }
    stages {
        stage('Deploy to Remote') {
            steps {
                script {
                    def remote = [:]
                    remote.name = 'staging'
                    remote.host = "${staging_server}"
                    remote.user = ssh_username
                    remote.password = ssh_password
                    remote.port = staging_port

                    sh '''
                        cd ${WORKSPACE}
                        find . -type f -mmin -10 -not -path "./.git/*" -not -name "Jenkinsfile" | while read fileName
                        do
                            fil=$(echo ${fileName} | sed 's:${WORKSPACE}/::')
                            scp -r ${fileName} ${remote.user}@${remote.host}:/var/www/html${fil}
                        done
                    '''
                }
            }
        }
    }
}
