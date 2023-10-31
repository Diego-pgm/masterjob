@Library('shared_library@feature-trigger-job')_

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
          script{
            def jobPath = "mule/first-api"
            def parameters = [
              "${params.env}"
              "${params.region}"
              "${params.BRANCH}"
            ]
            def triggeredBuild = runJob(jobPath, parameters)
            println("Triggered build number: ${triggeredBuild?.number}")
          }
            
        }
    }
  }
}
