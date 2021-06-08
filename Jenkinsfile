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
        
        stage('npm build'){
            steps{
                cd DotnetTemplate.Web
                npm run build --if-present
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

    agent {
        docker {image 'mcr.microsoft.com/dotnet/sdk'}
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
        
        stage('dotnet test'){
            steps{
                dotnet test
            }
        }
    }
}