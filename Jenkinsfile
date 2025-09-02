pipeline {
    agent any
    tools {
      maven 'Maven-3.9.11'
    }
    stages {
        stage('Source') {
            steps {
                git branch: 'main',
                    changelog: false,
                    poll: false,
                    url: 'https://github.com/maria-efimova/publish-reports.git'
            }
        }
        stage('Clean') {
            steps {
                dir("${env.WORKSPACE}"){
                    sh 'mvn clean'
                }
            }
        }
        stage('Test') {
            steps {
                dir("${env.WORKSPACE}"){
                    sh 'mvn test'
                }
            }
        }
        stage('Package') {
            steps {
                dir("${env.WORKSPACE}"){
                    sh 'mvn package -DskipTests'
                }
            }
        }
    }
    post {
        always {
            junit allowEmptyResults: true,
                testResults: '**/TEST-com.learningjenkins.AppTest.xml'

            archiveArtifacts allowEmptyArchive: true,
                artifacts: '**/hello-1.0-SNAPSHOT.jar'
        }
    }
}