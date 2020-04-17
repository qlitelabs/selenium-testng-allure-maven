pipeline{
    agent{
        docker {
            image 'maven:3-alpine'
            args '-v /Users/ankurshah/.m2:/root/.m2'
        }
    }
    stages{
        stage('Build') {
            steps {
                sh 'mvn clean verify -P grid -DsuiteXmlFile=smoke.suite.xml'
                junit allowEmptyResults: true testResults: 'target/surefire-reports/*.xml']
            }
            post {
                always {
                    allure results: [[path: 'target/allure-results']]
                    deleteDir()
                }
                success{
                    echo "========A execution successful========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
    }
}