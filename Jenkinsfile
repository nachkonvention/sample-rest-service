node {
  stage 'Checkout'
  checkout scm

  stage 'Build'
  echo "Building branch is: ${env.BRANCH_NAME}"
  def mvnHome = tool 'maven-3'
  sh "${mvnHome}/bin/mvn clean install -DskipTests"

  stage 'Archive'
  archiveArtifacts artifacts: 'target/**/*'
}