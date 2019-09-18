pipeline {
    agent {
        label 'Master'
    }

    options {
        disableConcurrentBuilds()
    }

    stages {
        stage("Checkout") {
            steps {
                checkout scm
            }
        }


        stage("Unit Test") {
            steps {
                sh "chmod +x mvnw"
                sh "./mvnw clean test -DskipITs=true -Dcheckstyle.skip=true"
            }
        }

        stage("Integration Test") {
            steps {
                sh "./mvnw verify -Dsurefire.skip=true"
            }
        }


        stage('Publish') {
            steps {
                junit '**/target/surefire-reports/*.xml'
            }
        }

    }

    post {

        cleanup {
            cleanWs()
        }
    }
}