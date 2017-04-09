node {
    def mvnHome = tool 'maven-3'

    stage ('Checkout') {
        checkout scm
    }

    stage ('Build') {
        echo "Building branch is: ${env.BRANCH_NAME}"
        sh "${mvnHome}/bin/mvn clean install -DskipTests"
    }
}