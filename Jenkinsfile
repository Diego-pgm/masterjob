pipeline{
  agent { label 'ubuntu'}
  options { buildDiscarder(logRotator(numToKeepStr: '5'))}
  parameters {
    choice(choices: ['GSDEV', 'GSUAT', 'GSPRD'], name:'env', description: 'Environment to deploy')
    choice(choices: ['us-east-2', 'us-east-1'], name: 'region')
    gitParameter(
      branchFilter: 'origin/(.*)',
      defaultValue: 'master',
      name: 'BRANCH',
      type: 'PT_BRANCH'
    )
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
            build wait: false, 
                  propagate: false, 
                  job: '/mule/first-api', 
                  parameters: [
                    string(name: 'env', value: 'GSDEV'), 
                    string(name: 'region', value: 'us-east-2'), 
                    gitParameter(name: 'BRANCH', value: 'master')]
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
