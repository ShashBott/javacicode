pipeline {
    agent any

    stages {
        stage('GIT Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/Vidhant007/javaci-project.git'
            }
        }

        stage('UNIT TESTING') {
            steps {
                sh 'mvn test'
            }
        }

        stage('INTEGRATION TESTING') {
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }

        stage('BUILD') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('STATIC CODE ANALYSIS') {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'key') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }

        stage('QUALITY GATE STATUS') {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'key'
                }
            }
        }

    }
}
