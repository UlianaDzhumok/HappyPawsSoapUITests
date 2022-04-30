pipeline {
    options {
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '50', artifactNumToKeepStr: '50'))
    }

    agent any

    tools {
        maven 'maven3'
        jdk 'jdk8'
        allure 'allure2'
    }

    triggers {
        pollSCM 'H/5 * * * *'
          cron '''TZ=Europe/Oslo
        H H(13-14) * * *'''
    }

    stages {
        stage('Test') {
            steps {
                sh '''
                    mvn clean test
                '''
            }
            post {
                always {
                    archiveArtifacts 'target/surefire-reports/**/*.xml'
                    junit 'target/surefire-reports/**/*.xml'
                }
            }
         }
    }
}