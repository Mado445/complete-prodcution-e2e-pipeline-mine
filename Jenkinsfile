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

        stage("Build App"){
            steps{
                sh "mvn clean package"
            }
        }

        stage("Test App"){
            steps{
                sh "mvn test"
            }
        }
        stage("sonarqube analysis"){
            script {
                steps{
                    withSonarQubeEnv(credentialsId: 'jenkiins-sonarqube-token'){
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }

    }



}