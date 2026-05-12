pipeline {
agent any
triggers {
pollSCM('H/2 * * * *')
}
environment {
// Ensure the name 'NodeJS' matches exactly what you setup in Step 2
NODEJS_HOME = tool name: 'NodeJS', type:
'jenkins.plugins.nodejs.tools.NodeJSInstallation'
// Append Node to PATH (Windows syntax)
PATH = "${env.NODEJS_HOME};${env.PATH}"
// Use a Windows path for deployment (e.g., C:\jenkins-deploy\my-app)
DEPLOY_DIR = 'C:\\jenkins-deploy\\my-app'
}
stages {
stage('Clone Repository') {
steps {

echo 'Cloning...'
git branch: 'master', url:
'https://github.com/a250028/SimpleNodejsPrj01.git'
}
}
stage('Install Dependencies') {
steps {
echo 'Installing dependencies...'
// Use 'bat' for Windows commands instead of 'sh'
bat 'npm install'
}
}
stage('Deploy to Local Server') {
steps {
echo 'Deploying...'
// Windows commands using 'bat'
bat """
mkdir ${DEPLOY_DIR}
xcopy /E /I /Y . ${DEPLOY_DIR}
cd ${DEPLOY_DIR}
npm install
pm2 restart my-app || pm2 start server.js --name my-app
"""
}
}
}
}
