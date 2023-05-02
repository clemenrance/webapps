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
    }
}