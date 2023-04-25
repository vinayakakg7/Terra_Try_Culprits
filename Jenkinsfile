pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/vinayakakg7/Terra_Try_Culprits.git']]])

                script {

                // Retrieve the culprits
                def changeLogSets = currentBuild.rawBuild.changeSets
                def culprits = []

                for (changeLogSet in changeLogSets) {
                    for (entry in changeLogSet) {
                        def commit = entry.commitId
                        def author = bat (returnStdout: true, script: "git show -s --format='%an <%ae>' ${commit}")
                        culprits.add(author.trim())
                    }
                  }
                }

                // Send the email
                emailext (
                    to: "vinayaka.kg@cyqurex.com",
                    subject: "Build notification",
                    body: "Build triggered by ${env.CHANGE_AUTHOR} has completed. Culprits: ${culprits.join(', ')}",
                    attachLog: true
                )
            }
        }

        stage('Build') {
            steps {
				echo "Build successfull"
            }
        }
    }
}
