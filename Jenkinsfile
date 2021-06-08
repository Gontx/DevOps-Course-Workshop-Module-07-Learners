pipeline{
    agent none
    stages{
        stage('Checkout'){
            steps{
                checkout scm
            }
        } 
        stage('npm build'){
            agent{
                docker {image 'node:14-alpine'}
            }
            steps{
                dir('DotnetTemplate.Web'){
                    echo "Building node..."
                    sh "npm install"
                    sh "npm run build --if-present"
                    echo "Testing node..."
                    sh "npm t"
                    sh "npm run lint"
                } 
            }
        }
        stage('DotNet build'){
            agent {
                docker {image 'mcr.microsoft.com/dotnet/sdk'}
            }
            environment{
                DOTNET_CLI_HOME = "/tmp/dotnet_cli_home"
            }
            steps{
                echo "Building dotnet..."
                sh "dotnet build"
                echo "Testing dotnet..."
                sh "dotnet test"
                echo "Finishing"
            }
        }
    }
}