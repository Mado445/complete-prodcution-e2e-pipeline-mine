pipeline{
    agent{
        label "jenkins-agent"
    }

    tools{
        jdk "Java17"
        maven "Maven3"
    }

    stages{
        stage("Cleanup Workspace"){
            steps{
                cleanWs()
            }
        }

        stage("Checkout from SCM"){
            steps{
                git branch: 'main', credentialsId: 'github-ref', url: 'https://github.com/Mado445/complete-prodcution-e2e-pipeline-mine'
            }

        }
    }



}