pipeline{
  agent any
  stages{
    stage('dev-deploy'){
      when {
        branch "dev"
      }
      steps{
        echo "deploy to dev environment"
      }
    }
    stage('uat-deploy'){
      when {
        branch "uat"
      }
      steps{
        echo "deploy to uat environment"
      }
    }
    stage('prd-deploy'){
      when {
        branch "main"
      }
      steps{
        echo "deploy to prd environment"
      }
    }
  }
}
