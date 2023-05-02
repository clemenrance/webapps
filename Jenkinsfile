pipeline{

    agent any

    stages{

        stage('Continouse Download'){

            steps{
                git branch: 'main', url: 'https://github.com/clemenrance/webapps.git'
            }
        }
        stage('Unit Test'){

            steps{
                sh 'mvn test'
            }
        }
        stage('Integration Test'){

            steps{
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage('Continouse Build'){

            steps{

                sh 'mvn clean install'
            }
        }
        stage ('Static Test'){

            steps{

                script{
                   withSonarQubeEnv(credentialsId: 'sonar-auth'){
                    sh 'mvn clean package sonar:sonar'
                   } 
                }
            }
        }
        stage('Quality Gate'){

            steps{

                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-auth'
                }
            }
        }
        stage('Nexus Uplod')

            steps{

                script{
                  nexusArtifactUploader artifacts: [[artifactId: 'maven-project', classifier: '', file: 'target/Maven-Project.war', type: 'war']], credentialsId: 'nexus-link', groupId: 'com.example.maven-project', nexusUrl: '3.93.153.108:9000', nexusVersion: 'nexus3', protocol: 'http', repository: 'webapp', version: '1.0-SNAPSHOT'  
                }
            }
        }
    }
}