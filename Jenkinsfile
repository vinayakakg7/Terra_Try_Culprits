pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/vinayakakg7/Terra_Try_Culprits.git']]])
            }
        }
        stage('Get Latest Commit') {
            steps {
                script {
                    def git = bat(returnStdout: true, script: 'git rev-parse HEAD').trim()
                    def author = bat(returnStdout: true, script: git log -1 --pretty="%an: %s").trim()
                 //   def message = bat(returnStdout: true, script: 'git log -1 --pretty="%s"').trim()
                    def commit_info = "Last Commit:\nAuthor: ${author}\nMessage: ${message}\nCommit SHA: ${git}"
                    env.commit_info = commit_info
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
