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
        
        stage('Upload Artifacts to Nexus'){
            
            steps{

                script{

                    nexusArtifactUploader artifacts: 
                [
                    [
                    artifactId: 'springboot',
                    classifier: '', 
                    file: 'target/UPES.jar', 
                    type: 'jar'
                    ]
                ], 
                    credentialsId: 'nexuscreds', 
                    groupId: 'com.example', 
                    nexusUrl: '13.233.118.188:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'nexus-repo', 
                    version: '1.0.0'
                }
            }
        }

    }
}
