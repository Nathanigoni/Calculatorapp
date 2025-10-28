pipeline {
    agent any

    stages {
        stage("Compile") {
            steps {
                bat "mvn clean compile"
            }
        }

        stage("Unit Test") {
            steps {
                bat "mvn clean test"
            }
        }
        stage("Code Coverage") {
            steps {
                // Run tests and generate JaCoCo report
                sh "mvn clean test jacoco:report"

                // Verify code coverage thresholds (as defined in pom.xml)
                sh "mvn jacoco:check"
            }
        }
        stage("Code Coverage") {
            steps {
                // Run tests and generate JaCoCo coverage report
                sh "mvn clean test jacoco:report"

                // Publish the JaCoCo HTML report in Jenkins
                publishHTML(target: [
                    reportDir: 'target/site/jacoco',
                    reportFiles: 'index.html',
                    reportName: 'JaCoCo Report'
                ])

                // Enforce coverage rules from pom.xml
                sh "mvn jacoco:check"
            }
        }
        stage("Triggers") {
           triggers {
            pollSCM('* * * * *')
           }
        }


    }
}
