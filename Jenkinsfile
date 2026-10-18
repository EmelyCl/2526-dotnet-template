pipeline {
    agent {
        docker{
            image 'mcr.microsoft.com/dotnet/sdk:10.0'
            reuseNode true
        }
    }

    stages{
        stage('Restore .NET app'){
            steps {
                sh 'dotnet restore Rise.sln'
            }
        }
        stage ('Build .NET app'){
            steps{
                sh 'dotnet build Rise.sln --no-restore'
            }
        }
        stage ('Test .NET app'){
            steps{
                sh 'dotnet test Rise.sln'
            }
        }
    }
}