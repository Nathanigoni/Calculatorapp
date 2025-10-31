pipeline {
    agent any

    // Triggers should be defined here, outside stages
    triggers {
        pollSCM('* * * * *')  // checks every minute
    }

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

//         stage("Code Coverage") {
//             steps {
//                 // Run tests and generate JaCoCo report
//                 bat "mvn clean test jacoco:report"
//
//                 // Publish the JaCoCo HTML report
//                 publishHTML(target: [
//                     reportDir: 'target/site/jacoco',
//                     reportFiles: 'index.html',
//                     reportName: 'JaCoCo Report'
//                 ])
//
//                 // Enforce coverage thresholds defined in pom.xml
//                 bat "mvn jacoco:check"
//             }
//         }
    }

    post {
        always {
            mail to: 'usnow02@gmail.com',
            subject: "Completed Pipeline: ${currentBuild.fullDisplayName}",
            body: "Your build completed, please check: ${env.BUILD_URL}"
        }
    }
}
