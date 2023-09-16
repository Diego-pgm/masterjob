pipeline{
  agent { label 'ubuntu'}
  options { buildDiscarder(logRotator(numToKeepStr: '5'))}
  parameters {
    booleanParam(name: 'firstapi', defaultValue: false, description: '')
    booleanParam(name: 'secondapi', defaultValue: false, description: '')
    booleanParam(name: 'thirdapi', defaultValue: false, description: '')
    booleanParam(name: 'fourthapi', defaultValue: false, description: '')
    booleanParam(name: 'fifthapi', defaultValue: false, description: '')
  }
  stages{
    stage('Deploy APIs'){
      steps{
        script{
          if (params.firstapi){
            build wait: false, job: 'mule/first-api'
          }
          if (params.secondapi){
            build wait: false, job: 'mule/second-api'
          }
          if (params.thirdapi){
            build wait: false, job: 'mule/third-api'
          }
          if (params.fourthapi){
            build wait: false, job: 'mule/fourth-api'
          }
          if (params.fifthapi){
            build wait: false, job: 'mule/fifth-api'
          }
        }
      }
    }
  }
}
