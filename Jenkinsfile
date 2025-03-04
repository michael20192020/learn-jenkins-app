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
                dir
                curl -o nodejs.zip https://nodejs.org/dist/v23.9.0/node-v23.9.0-win-x64.zip
                tar -xf nodejs.zip
                set PATH=%CD%\\node-v23.9.0-win-x64;%PATH%   
                
                node --version
                npm --version
                npx npm@latest help ci
                npm ci --loglevel verbose
                npm run build
                dir
                '''
               

            }
        }
    }
}
