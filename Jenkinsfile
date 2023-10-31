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
    stage('Prepare'){
      steps{
        script{
          currentBuild.displayName = "${params.env}-${params.BRANCH}-${BUILD_NUMBER}"
          currentUser = currentBuild.getBuildCauses()[0].userId
          if (!(currentUser ==~ /(dperez)/)){
            error "User ${currentUser} is not allowed to deploy"
          }
        }
      }
    }
    stage('test'){
        steps{
           sayHello 'Diego'
        }
    }
    stage('Deploy APIs'){
      steps{
        script{
          if (params.firstapi){
            build wait: false, propagate: false, job: '/mule/first-api', parameters: [string(name: 'env', value: "${params.env}"), string(name: 'region', value: "${params.region}"), gitParameter(name: 'BRANCH', value: "${params.BRANCH}"), string(name: 'currentUser', value: "${currentUser}")]}
          if (params.secondapi){
            build wait: false, propagate: false, job: 'mule/second-api', parameters: [string(name: 'env', value: "${params.env}"), string(name: 'region', value: "${params.region}"), gitParameter(name: 'BRANCH', value: "${params.BRANCH}"), string(name: 'currentUser', value: "${currentUser}")]}
          if (params.thirdapi){
            build wait: false, propagate: false, job: 'mule/third-api', parameters: [string(name: 'env', value: "${params.env}"), string(name: 'region', value: "${params.region}"), gitParameter(name: 'BRANCH', value: "${params.BRANCH}"), string(name: 'currentUser', value: "${currentUser}")]}
          if (params.fourthapi){
            build wait: false, propagate: false, job: 'mule/fourth-api', parameters: [string(name: 'env', value: "${params.env}"), string(name: 'region', value: "${params.region}"), gitParameter(name: 'BRANCH', value: "${params.BRANCH}"), string(name: 'currentUser', value: "${currentUser}")]}
          if (params.fifthapi){
            build wait: false, propagate: false, job: 'mule/fifth-api', parameters: [string(name: 'env', value: "${params.env}"), string(name: 'region', value: "${params.region}"), gitParameter(name: 'BRANCH', value: "${params.BRANCH}"), string(name: 'currentUser', value: "${currentUser}")]}
        }
      }
    }
  }
}
