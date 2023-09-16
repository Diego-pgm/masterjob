pipeline{
  agent { label 'ubuntu'}
  parameters {
    booleanParam(name: 'api1', defaultValue: false, description: '')
    booleanParam(name: 'api2', defaultValue: false, description: '')
    booleanParam(name: 'api3', defaultValue: false, description: '')
  }
  stages{
    stage('Deploy APIs'){
      steps{
        script{
          if (params.api1){
            build wait: false, job: 'mule/first-api'
          }
          if (params.api2){
            build wait: false, job: 'mule/second-api'
          }
          if (params.api3){
            build wait: false, job: 'mule/third-api'
          }
        }
      }
    }
  }
}
