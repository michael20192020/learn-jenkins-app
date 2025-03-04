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
                REM curl -o nodejs.zip https://nodejs.org/dist/v18.17.1/node-v18.17.1-win-x64.zip
                REM tar -xf nodejs.zip
                REM set PATH=%CD%\\node-v18.17.1-win-x64;%PATH%
                set PATH=D:\\Program Files\\nodejs;%PATH%
                node --version
                npm --version
                npm ci
                npm run build
                dir
                '''
                

            }
        }
    }
}
