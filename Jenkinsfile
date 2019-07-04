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
               url: 'https://TfNSWAnyCloud@dev.azure.com/TfNSWAnyCloud/AnyCloud_Foundation/_git/AnyCloud_Foundation',
               credentialsId: 'AzureDevOpsCredentialHttps',
               branch: "jenkins_test"
            )

          dir('LogicApps/creationResourceGroup'){
            sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
            sh 'az group deployment create --name testLogicAppDeployment --resource-group testGroupName --template-file template.json'
          }
      }
    }
  }
}
}
