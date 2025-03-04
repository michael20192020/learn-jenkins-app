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
                    args '-it --entrypoint powershell'
                    reuseNode true
                }
            }
            steps {
                
                bat '''
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
