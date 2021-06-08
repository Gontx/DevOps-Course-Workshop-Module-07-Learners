pipeline{
    stages{
        stage('Checkout'){
            steps{
                checkout scm
            }
        } 
        stage('npm build'){
            agent {
                docker {image 'node:14-alpine'}
             }
            steps{
                dir('DotnetTemplate.Web'){
                    sh "npm run build --if-present"
                    sh "npm run lint"
                } 
            }
        }
        stage('DotNet build'){
            agent {
                docker {image 'mcr.microsoft.com/dotnet/sdk'}
            }
            steps{
                sh "dotnet build"
                sh "dotnet test"
            }
        }
    }
}