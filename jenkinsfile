pipeline{
    agent {
        docker {image 'node:14-alpine'}
    }
    stages{
        stage('Checkout'){
            steps{
                checkout scm
            }
        }

        stage('Dotnet Build'){
            steps{
                dotnet build
            }
        }
        
        stage('npm install and build'){
            steps{
                cd DotnetTemplate.web
                npm install
                npm run build --if-present
            }
        }
        
        stage('dotnet test'){
            steps{
                dotnet test
            }
        }
        
        stage('Node test'){
            steps{
                cd DotnetTemplate.Web
                npm t
            }
        }
        
        stage('Node lint test'){
            steps{
                npm run lint
            }
        }
    }
}