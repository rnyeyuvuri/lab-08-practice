pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'java -version'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B clean package -Dmaven.compiler.release=17'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -B test -Dmaven.compiler.release=17'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
