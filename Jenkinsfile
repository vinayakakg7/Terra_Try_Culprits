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
                script {
                 // Retrieve the author of the most recent commit
                        def changeLogSets = currentBuild.rawBuild.changeSets
                        def culprits = []

                        for (changeLogSet in changeLogSets) {
                            for (entry in changeLogSet) {
                                def commit = entry.commitId
                                def author = bat(returnStdout: true, script: "git show -s --format='%an <%aE>' ${commit}")
                                echo "Commit: ${commit}, Author: ${author}"
                                culprits.add(author.trim())
                            }
                        }

                            // Send the email
                            emailext (
                                to: "",
                                subject: "Build notification",
                                body: "Build triggered by ${env.CHANGE_AUTHOR} has completed. Culprits: ${culprits.join(', ')}",
                                attachLog: true
                            )
                }
            }
        }
    
    }
}
