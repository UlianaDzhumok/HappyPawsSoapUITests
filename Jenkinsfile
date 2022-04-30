pipeline {
    options {
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '50', artifactNumToKeepStr: '50'))
    }

    agent any

    tools {
           maven "MAVEN"
           jdk "JDK"
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