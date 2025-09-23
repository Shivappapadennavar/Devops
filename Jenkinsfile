pipeline {
    agent any

    tools {
        nodejs "nodejs18" // <-- must match the name from Global Tool Config
    }

    environment {
        APP_NAME = "my-node-app"
        BUILD_ARTIFACT = "build.zip"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Shivappapadennavar/Devops.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Artifact') {
            steps {
                sh '''
                    zip -r ${BUILD_ARTIFACT} . \
                    -x "node_modules/*" \
                    -x ".git/*"
                '''
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: "${BUILD_ARTIFACT}", fingerprint: true
            }
        }
    }

    post {
        success {
            echo "✅ Build succeeded for ${APP_NAME}"
        }
        failure {
            echo "❌ Build failed for ${APP_NAME}"
        }
    }
}


