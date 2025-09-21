pipeline{
    agent{
        label "jenkins-agent"
    }

    tools{
        jdk "Java17"
        maven "Maven3"
    }
    environment{
        APP_NAME="complete-prodcution-e2e-pipeline-mine"
        RELEASE="1.0.0"
        DOCKER_USER="mado445555"
        DOCKER_PASS="dockerhub"
        IMAGE_NAME="${DOCKER_USER}"+"/"+"${APP_NAME}"
        IMAGE_TAG="${RELEASE}-${BUILD}"

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
            steps {
                script{
                    withSonarQubeEnv(credentialsId: 'jenkiins-sonarqube-token'){
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }

        stage("quality gate sonar webhook"){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'jenkiins-sonarqube-token'

                }
            }


        }

        stage("docker build and push"){
            steps{
                script{
                    docker.withRegistry('',DOCKER_PASS,){
                        docker_image=docker.build"${IMAGE_NAME}"
                    }
                    docker.withRegistry('',DOCKER_PASS){
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }

                }
            }
        }

    }



}