pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh './gradlew build'
            }
        }
        stage('Test') {
            steps {
                echo 'Generating Test Report..'
                sh './gradlew -i test jacocoTestReport --stacktrace'
            }
        }
        stage('Analyze') {
            environment {
                SONARQUBE_PROYECT  = credentials('sonarqube-project')
                SONARQUBE_URL = credentials('sonarqube-url')
                SONARQUBE_TOKEN = credentials('sonarqube-token')
            }
            steps {
                echo 'Analyze..'
                sh './gradlew sonarqube -Dsonar.projectKey=$SONARQUBE_PROYECT -Dsonar.host.url=$SONARQUBE_URL -Dsonar.login=$SONARQUBE_TOKEN --stacktrace'
            }
        }
    }
}