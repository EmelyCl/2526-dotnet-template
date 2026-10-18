pipeline {
    agent {
        docker{
            image 'mcr.microsoft.com/dotnet/sdk:9.0'
            reuseNode true
        }
    }
    
    triggers {
        pollSCM('H/2 * * * *') 
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
        stage('Deploy'){
            agent {
                docker {
                    image 'docker:cli'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                    reuseNode true
                }
            }
            steps {
                sh 'docker compose down'
                sh 'docker compose up -d --build'
            }
        }
    }
}