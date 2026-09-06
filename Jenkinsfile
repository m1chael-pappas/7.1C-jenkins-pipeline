pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Task: Compile and package the application into a deployable artefact.'
                echo 'Tool: Maven (mvn clean package)'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Task: Run unit tests to verify individual components, then integration tests to verify components work together.'
                echo 'Tools: JUnit for unit tests, Selenium for integration tests'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Task: Analyse source code for bugs, code smells, and standards violations.'
                echo 'Tool: SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Task: Scan dependencies and code for known vulnerabilities (CVEs).'
                echo 'Tool: OWASP Dependency-Check'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Task: Deploy the packaged artefact to a staging server.'
                echo 'Tool: AWS CLI / AWS CodeDeploy to an EC2 instance'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Task: Run end-to-end integration tests against the staging environment.'
                echo 'Tool: Postman/Newman for API tests, Selenium for UI tests'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Task: Deploy the verified artefact to the production server.'
                echo 'Tool: AWS CLI / AWS CodeDeploy to a production EC2 instance'
            }
        }
    }
}
