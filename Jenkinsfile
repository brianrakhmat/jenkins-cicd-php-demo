pipeline{
    agent any
    environment{
        staging_server="103.30.195.241"
    }
    stages{
        stage('Deploy to Remote'){
            steps{
                sh '''
                    for fileName in `find ${WORKSPACE} -type f -mmin -10 | grep -v ".git" | grep -v "Jenkinsfile"`
                    do
                        fil=$(echo ${fileName} | sed 's/'"${JOB_NAME}"'/ /' | awk {'print $2'})
                        scp -r ${WORKSPACE}${fil} itopr@${staging_server}:/var/www/html${fil}
                    done
                '''
            }
        }
    }
}
