pipeline{
  agent { label 'ubuntu'}
  parameters {
    booleanParam(name: 'first-api', defaultValue: false, description: '')
    booleanParam(name: 'second-api', defaultValue: false, description: '')
    booleanParam(name: 'third-api', defaultValue: false, description: '')
  }
  stages{
    stage('Deploy APIs'){
      steps{
        script{
          if (params.first-api){
            build wait: false, job: 'mule/first-api'
          }
          if (params.second-api){
            build wait: false, job: 'mule/second-api'
          }
          if (params.third-api){
            build wait: false, job: 'mule/third-api'
          }
        }
      }
    }
  }
}
