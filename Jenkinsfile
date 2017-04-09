@Library('sample-pipeline-libraries@master') _

node {
    def mvnHome = tool 'maven-3'
    isMaster()

    stage ('Checkout') {
        checkout scm
    }

    stage ('Build') {
        echo "Building branch is: ${env.BRANCH_NAME}"
        sh "${mvnHome}/bin/mvn clean install -DskipTests"
    }

}