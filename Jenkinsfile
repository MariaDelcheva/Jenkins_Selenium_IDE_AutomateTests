pipeline {
    agent any

    stages{
        stage("Checkout code"){
          // checkout the repository 
            steps {
                git branch: 'main', url: 'https://github.com/MariaDelcheva/Jenkins_Selenium_IDE_AutomateTests'
            }
        }

        stage("Set uo .Net Core"){
           
            steps {
                bat '''
                echo Downloading .Net 6 Sdk
                curl -l -o dotnet-sdk-6.0.132-win-x64.exe https://download.visualstudio.microsoft.com/download/pr/23c7bf0d-e22d-4372-bcb2-292eb36a5238/11af494be409759f46b679ab22e65a58/dotnet-sdk-6.0.424-win-x64.exe
                echo installing dotnet-sdk-6.0.132-win-x64.exe
                dotnet-sdk-6.0.132-win-x64.exe /quiet/norestart
                '''
            }
        }

        stage("Restoring nuget packages"){
           
            steps {
                bat 'dotnet restore SeleniumIde.sln' 
            }
        }

        stage("Build"){
           
            steps {
                bat 'dotnet build SeleniumIde.sln --configuration Release' 
            }
        }

        stage("Run Tests"){
           
            steps {
                bat 'dotnet test SeleniumIde.sln --logger "trx;LogFileName=TestResults.trx"' 
            }
        }
 
    }

    post {
       always{
            arhiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: TestResults
            step([
               $class: 'MSTestPublisher',
               testResultsFile: '**/TestResults/*.trx'
            ])
       }
    }
}