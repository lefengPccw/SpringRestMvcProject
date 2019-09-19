pipeline {
    agent { docker { image 'maven:3.3.3' } }
    stages {
        stage('check java') {
            steps {
                sh "java -version"
            }
        }

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
                sh "mvn verify -Dsurefire.skip=true"
            }
        }


        stage('Publish') {
            steps {
                junit '**/target/surefire-reports/*.xml'
                step( [ $class: 'JacocoPublisher' ] )
            }
        }

    }

    post {

        cleanup {
            cleanWs()
        }
    }
}