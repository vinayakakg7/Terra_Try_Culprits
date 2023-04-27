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
                    def changes = CHANGES_SINCE_LAST_SUCCESS
                    def commit_hash = sh(script: 'git rev-parse HEAD', returnStdout: true).trim()
                    def author_name = sh(script: 'git log -1 --pretty=format:"%an"', returnStdout: true).trim()
                    env.commit_info = "Last Commit:\nAuthor: ${author_name}\n\nMessage:\nCommit SHA: ${commit_hash}"
                }
            }
        }
        stage('Send Email Notification') {
            steps {
                emailext body: "${changes}",
                         //body: "${env.commit_info}", 
                         subject: 'Latest Commit Information',
                         to: 'vinayaka.kg@cyqurex.com',
                         mimeType: 'text/html'
                        
            }
        }
        
    }
}
