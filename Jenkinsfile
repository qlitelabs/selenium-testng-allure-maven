pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean verify -P grid -DsuiteXmlFile=smoke.suite.xml'
            }
        }
    }
    post {
        always {
            allure results: [[path: 'target/allure-results']]
            junit 'target/surefire-reports/*.xml'
            deleteDir()
        }
    }
}