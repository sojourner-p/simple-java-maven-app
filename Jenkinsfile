pipeline {
    agent any
    tools {
        // This name MUST match the Name you gave it in Manage Jenkins > Tools
        maven 'maven-3.9'
    }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'  // Shows test results in Jenkins UI
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'  // Simple delivery script included in repo
            }
        }
    }
}