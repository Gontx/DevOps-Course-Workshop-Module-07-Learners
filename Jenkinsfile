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
                    echo "Building node..."
                    sh "npm run build --if-present"
                    echo "Testing node..."
                    sh "npm run lint"
                } 
            }
        }
        stage('DotNet build'){
            agent {
                docker {image 'mcr.microsoft.com/dotnet/sdk'}
            }
            steps{
                echo "Building dotnet..."
                sh "dotnet build"
                echo "Testing dotnet..."
                sh "dotnet test"
            }
        }
    }
}