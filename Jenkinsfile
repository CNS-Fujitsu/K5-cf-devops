#!groovy


node {

    currentBuild.result = "SUCCESS"

    
    try {
    stage 'Checkout'
          // Checkout scm
          sh 'git clone https://github.com/fujitsuk5/K5-cf-devops.git'
   
    stage 'Build'
  
          // Execute build

          sh 'npm install'

    stage 'Test'

          sh 'npm test'
        }

    catch (err) {
      currentBuild.result = "SUCCESS"
    }    

}

node {
    stage 'Deploy Web App On CloudFoundry'
    
    try { 
      wrap([$class: 'CloudFoundryCliBuildWrapper',
          cloudFoundryCliVersion: 'Cloud Foundry CLI (built-in)',
          apiEndpoint: 'https://api.uk-1.paas-cf.cloud.global.fujitsu.com',
          skipSslValidation: true,
          credentialsId: 'CF creds',
          organization: 'YssmW1yI',
          space: 'development']) {

             sh 'cf push myapp-dev'
          }
       }

    catch (err) {
      currentBuild.result = "SUCCESS"
    }    

}


