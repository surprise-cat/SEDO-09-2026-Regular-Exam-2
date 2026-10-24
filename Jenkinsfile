pipeline {
    agent any

    environment {
        DOTNET_CLI_TELEMETRY_OPTOUT = '1'
        BUILD_CONFIGURATION = 'Release'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Restore') {
            steps {
                echo 'Restoring NuGet packages...'
                sh 'dotnet restore'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the .NET application...'
                sh "dotnet build --configuration ${env.BUILD_CONFIGURATION} --no-restore"
            }
        }
        stage('Test') {
            steps {
                echo 'Executing unit and integration tests...'
                sh "dotnet test --configuration ${env.BUILD_CONFIGURATION} --no-build --verbosity normal"
            }
        }
    }
}
