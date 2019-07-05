pipeline {
  agent any
  
  options {
    timestamps()
    ansiColor('xterm')
  }

  environment {
    PATH="/usr/local/bin:$PATH"
  }

  stages {
    stage('Build') {
      steps {
        withCredentials([azureServicePrincipal('JenkinsServicePrincipal-paultest-ccoe')]) {
          sh 'rm -fr *'
          
            git(
               url: 'https://github.com/jackjiang317/testLogicApp.git',
               branch: "master"
            )
          
            sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
            sh 'az group deployment create --name testLogicAppDeployment --resource-group testGroupName --template-file jenkins_test.json'

        }
      }
    }
  }
}
