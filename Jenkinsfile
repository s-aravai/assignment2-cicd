pipeline {
    agent any

    environment {
        NETLIFY_TOKEN = credentials('NETLIFY_TOKEN')
        NETLIFY_SITE_ID = credentials('NETLIFY_SITE_ID')
        CI = 'true'
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test -- --watchAll=false'
            }
        }

        stage('Deploy') {
            steps {
                sh 'npx netlify-cli deploy --prod --dir=build --site=$NETLIFY_SITE_ID --auth=$NETLIFY_TOKEN'
            }
        }
    }
}