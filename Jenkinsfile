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
                curl -o nodejs.zip https://nodejs.org/dist/v18.17.1/node-v18.17.1-win-x64.zip
                tar -xf nodejs.zip
                set PATH=%CD%\\node-v18.17.1-win-x64;%PATH%   
                echo "start"
                node --version
                echo "before npm"
                npm --version || echo "npm version failed"
                echo "after npm"
                
                echo "keep alive"
                timeout /T 30
                echo "start run build"
                npm run build
                echo "end run build"
                dir
                echo "finish"
                '''
               

            }
        }
    }
}
