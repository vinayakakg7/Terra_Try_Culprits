pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/vinayakakg7/Terra_Try_Culprits.git']]])
            }
        }
        stage('Build') {
            steps {
				echo "Build successfull"
            }
        }
        stage('Email') {
            steps {
                script {
                // Retrieve the author of the most recent commit
                   def author = bat (returnStdout: true, script: 'git log -1 --pretty=format:"%an <%ae>"')

                // Send the email
                emailext to: "vinayaka.kg@cyqurex.com",
                         subject: "Build notification",
                         body: "Build triggered by ${env.CHANGE_AUTHOR} has completed. The author of the most recent commit is ${author}.",
                         attachLog: true
            }
         }
        }
    }
}
