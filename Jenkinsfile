pipeline {
    agent any

    environment {
        DOTNET_CLI_HOME = "C:\\Program Files\\dotnet"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                script {
                    // Restore the dependencies for the project
                    bat "dotnet restore"
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build the application in Release configuration
                    bat "dotnet build --configuration Release"
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run the tests (no restore, just using the existing dependencies)
                    bat "dotnet test --no-restore --configuration Release"
                }
            }
        }

        stage('Publish') {
            steps {
                script {
                    // Publish the application (output to the publish folder)
                    bat "dotnet publish --no-restore --configuration Release --output .\\publish"
                }
            }
        }
    }

    post {
        success {
            // Notify or log success message
            echo 'Build, test, and publish successful!'
        }
        failure {
            // Notify or log failure message
            echo 'Build, test, or publish failed!'
        }
    }
}
