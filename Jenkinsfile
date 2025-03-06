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
                set PATH=D:\\Program Files\\nodejs;%PATH%

                echo %PATH%
                
                echo "before npm"
                npm --version || echo "npm version failed"
                echo "after npm"

                

                dir
                curl -o nodejs.zip https://nodejs.org/dist/v18.17.1/node-v18.17.1-win-x64.zip
                tar -xf nodejs.zip
                set PATH=%CD%\\node-v18.17.1-win-x64;%PATH%   
                echo "start"
                node --version
                npm ci        
                npm run build

                dir
                echo "finish"
                '''
               

            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'mcr.microsoft.com/windows/servercore:ltsc2022'
                    reuseNode true
                }
            }
            steps {
                echo 'Test stage'
                sh '''
                  test -f package.json
                  npm test
                '''
            }

        }
    }

    post {
        always {
            junit 'test-result/junit.xml'
        }

    }
}
