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
                set PATH=D:\\Program Files\\nodejs;%PATH%
                "D:\\Program Files\\nodejs\\node" --version
                "D:\\Program Files\\nodejs\\npm" --version
                node --version
                npm --version
                npm ci || echo "npm ci failed"
                npm run build
                dir
                '''
                

            }
        }
    }
}
