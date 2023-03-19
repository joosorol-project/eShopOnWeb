pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '/opt/dotnet/dotnet build eShopOnWeb.sln'
      }
    }

    stage('Tests') {
      parallel {
        stage('Tests') {
          steps {
            sh '/opt/dotnet/dotnet test tests/UnitTests'
          }
        }

        stage('Integration') {
          steps {
            sh '/opt/dotnet/dotnet test tests/IntegrationTests'
          }
        }

        stage('Functional') {
          steps {
            sh '/opt/dotnet/dotnet test tests/FunctionalTests'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh '/opt/dotnet/dotnet publish eShopOnWeb.sln -O /var/aspnet'
      }
    }

  }
}