pipeline{
    agent{
        label "jenkins-agent"
    }

    tools{
        JDK "Java17"
        maven "Maven3"
    }

    stages{
        stage("Cleanup Workspace"){
            steps{
                CleanWs()
            }
        }

        stage("Checkout from SCM"){
            steps{
                git branch: 'main', credentialsId: 'github-ref', url: 'https://github.com/Mado445/complete-prodcution-e2e-pipeline-mine'
            }

        }
    }



}