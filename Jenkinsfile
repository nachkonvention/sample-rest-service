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

    stage ('metrics') {
        sh "${mvnHome}/bin/mvn findbugs:findbugs checkstyle:checkstyle pmd:pmd"

        step([$class: 'FindBugsPublisher', pattern: '**/findbugsXml.xml', unstableTotalAll:'0'])
        step([$class: 'hudson.plugins.checkstyle.CheckStylePublisher', pattern: '**/target/checkstyle-result.xml', unstableTotalAll:'0'])
        step([$class: 'PmdPublisher', pattern: '**/target/pmd.xml', unstableTotalAll:'0'])

        def scannerHome = tool 'Sonar-Scanner-3.0';
        withSonarQubeEnv('SonarQube-62') {
        sh "${scannerHome}/bin/sonar-scanner"
        }
    }
}