pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Build') {
            agent {
                docker {
                    image 'mcr.microsoft.com/windows/servercore:ltsc2022'
                    reuseNode true
                }
            }
            steps {
                
                bat '''
                ls -la
                curl -o nodejs.zip https://nodejs.org/dist/v18.17.1/node-v18.17.1-win-x64.zip
                tar -xf nodejs.zip
                set PATH=%CD%\\node-v18.17.1-win-x64;%PATH%
                node --version
                npm --version
                npm ci
                npm run build
                ls -la
                '''
                

            }
        }
    }
}
