pipeline{
    agent{
        label "jenkins-agent"
    }
    options {
        timeout(time: 30 , unit : 'MINUTES')
    }
    environment {
        NEXUS_URL = 'nexus.itindustry.online:8081'
        NEXUS_CREDENTIALS_ID = 'nexus-cred'
    }
    stages{
        stage("Zipping the code"){
            steps{
                sh """
                zip -r frontend.zip * -x Jenkinsfile
                """
            }
        }
        stage("Uploading artifact to nexus repo"){
            steps {
                script {
                    nexusArtifactUploader(
                        artifacts : [[
                            artifactId: 'frontend', // Replace with your artifact ID
                            classifier: '',
                            file: "frontend.zip",
                            type: 'zip'
                        ]],
                        credentialsId: "${env.NEXUS_CREDENTIALS_ID}",
                        groupId: 'com.expense', // Replace with your group ID
                        nexusUrl: "${env.NEXUS_URL}",
                        protocol: 'http',
                        repository: 'frontend-expense', // Replace with your repository name
                        //version: "${env.VERSION}"
                        nexusVersion: "nexus3"
                    )
                }
            }
        }
    }
}
