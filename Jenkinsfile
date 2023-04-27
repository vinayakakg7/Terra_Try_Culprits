pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/vinayakakg7/Terra_Try_Culprits.git']]])
            }
        }
       stage('Retrieve Latest Commit Information') {
            steps {
                script {
                    def commit_hash = bat(returnStdout: true, script: 'git rev-parse HEAD').trim()
                    def author_name = bat(returnStdout: true, script: 'git log -1 --pretty=format:"%an"').trim()
                    env.commit_info = "Last Commit:\nAuthor: ${author_name}\n\nMessage:\nCommit SHA: ${commit_hash}"
                }
            }
        }
        stage('Send Email Notification') {
            steps {
                emailext subject: 'Latest Commit Information',
                         body: "${env.commit_info}",
                         to: 'vinayaka.kg@cyqurex.com'
            }
        }
        
    }
}
