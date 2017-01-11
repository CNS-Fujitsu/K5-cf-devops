#!groovy


node {

    currentBuild.result = "SUCCESS"

    stage 'Checkout'
    
    try {
          # Checkout scm
          git clone https://github.com/fujitsuk5/K5-cf-devops.git
          # Execute build
          npm install 
        }
   
    stage 'Build'
  
    try {
          sh 'npm install'
        }

    stage 'Test'

    try {
          sh 'npm test'
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
}


