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
                        for fileName in `find ${WORKSPACE} -type f -mmin -10 | grep -v ".git" | grep -v "Jenkinsfile"`
                        do
                            fil=$(echo ${fileName} | sed 's/'"${JOB_NAME}"'/ /' | awk {'print $2'})
                            scp -r ${fileName} ${remote.user}@${remote.host}:${remote.port}:/var/www/html${fil}
                        done
                    '''
                }
            }
        }
    }
}
