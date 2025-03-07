pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = '5c858fb4-b8d6-4c04-b251-f0286bfec78a'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')

    }

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
                // npm ci        
                //npx update-browserslist-db@latest
                npm install --save-dev @babel/plugin-proposal-private-property-in-object
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
        stage('Deploy') {
            agent {
                docker {
                    image 'mcr.microsoft.com/windows/servercore:ltsc2022'
                    reuseNode true
                }
            }
            steps {
                echo 'Deploy stage'
                sh '''
                  npm install netlify-cli 
                  node_modules/.bin/netlify --version
                  echo "Deploy to production. Site ID: $NETLIFY_SITE_ID"
                  node_modules/.bin/netlify status
                  node_modules/.bin/netlify deploy --dir=build --prod
                '''
            }

        }
    }

    post {
        always {
            //publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false,reportDir:])
            junit 'test-result/junit.xml'
        }

    }
}
