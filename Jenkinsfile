pipeline{
    agent{
        docker {
            image 'maven:3-alpine'
            args '-v /Users/ankurshah/.m2:/root/.m2'
        }
    }
    stages{
        stage('Test') {
            steps {
                sh 'mvn clean verify -P grid -DsuiteXmlFile=smoke.suite.xml'
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                junit '**/target/surefire-reports/*.xml'
            }
            post {
                success{
                    echo "========A execution successful========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
        stage('Allure Reports') {
            steps {
                echo "===========Generating Allure Reports=============="
            }
            post {
                always {
                    allure results: [[path: 'target/allure-results']]
                    deleteDir()
                }
            }
        }
    }
}