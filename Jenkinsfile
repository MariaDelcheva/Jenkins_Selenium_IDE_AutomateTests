pipeline {
    agent any

    stages{
        stage("Checkout code"){
          // checkout the repository 
          steps {
             git branch: 'main', url: 'https://github.com/MariaDelcheva/Jenkins_Selenium_IDE_AutomateTests'
          }
        }
        stage("Set up .Net Core"){
          // install dot net  
        }
        stage("Restore dependencies"){
          // install dependencies
        }
        stage("Build"){
          // build
        }
        stage("Run Tests"){
          // run tests
        }
    }
}