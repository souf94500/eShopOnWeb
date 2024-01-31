pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'dotnet build eShopOnWeb.sln'
      }
    }

    stage('Tests') {
      parallel {
        stage('Tests') {
          steps {
            sh 'dotnet publish eShopOnWeb.sln -o /var/aspnet  -p:ErrorOnDuplicatePublishOutputFiles=false'
          }
        }

        stage('Integration') {
          steps {
            sh 'dotnet test tests/IntegrationTests'
          }
        }

        stage('Functional') {
          steps {
            sh 'dotnet test tests/FunctionalTests'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh ' dotnet publish eShopOnWeb.sln -o /var/aspnet  -p:ErrorOnDuplicatePublishOutputFiles=false'
      }
    }

  }
}