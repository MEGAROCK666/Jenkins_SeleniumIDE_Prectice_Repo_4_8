pipeline {
    agent any

    stages {
        stage("Checkout code") {
            steps {
                // Checkout code from GitHub and specify the branch
                git branch: 'main', url: 'https://github.com/MEGAROCK666/Jenkins_SeleniumIDE_Prectice_Repo_4_8'

            }
        }
        stage("Set up .NET Core") {
            steps {
                bat '''
                echo instaling .NET SDK 6.0
                choco install dotnet-sdk -y --version=6.0.100
                '''
            }
        }
        stage("Restore dependencies") {
            steps {
                // Restore dependencies using the solution file
                bat 'dotnet restore SeleniumIde.sln'
            }
        }
        stage("Build") {
            steps {
                // Build the project using the solution file
                bat 'dotnet build SeleniumIde.sln --configuration Release'
            }
        }
        stage("Run tests") {
            steps {
                // Run tests using the solution file
                bat 'dotnet test SeleniumIde.sln --logger "trx;LogFileName=TestResult.trx"'

            }
        }
    }
    post {
        aways {
            archiveArtifacts artifacts: '**/TestResults/*trx', allowEmptyArchive: true
            junit '**/TestResults/*.trx'
        }
    }
}