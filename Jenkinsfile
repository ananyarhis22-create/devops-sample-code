pipeline {
    agent any

    options {
        // Keep console tidy
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code from ${env.GIT_URL ?: 'local workspace'}"
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "=== BUILD STAGE ==="
                sh '''
                    echo "Simulating build..."
                    mkdir -p build
                    echo "Build artifact created at $(date)" > build/artifact.txt
                    ls -R
                '''
            }
        }

        stage('Test') {
            steps {
                echo "=== TEST STAGE ==="
                sh '''
                    echo "Running sample tests..."
                    # here you would run: mvn test / npm test / pytest etc.
                    echo "All tests passed ✅"
                '''
            }
        }

        stage('Package') {
            steps {
                echo "=== PACKAGE STAGE ==="
                sh '''
                    mkdir -p dist
                    cp build/artifact.txt dist/
                    echo "Packaged artifact into dist/ directory"
                    ls -R dist
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "=== DEPLOY STAGE ==="
                sh '''
                    echo "Deploying to DEV environment..."
                    sleep 2
                    echo "Deployment complete 🚀"
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline finished SUCCESSFULLY ✅"
        }
        failure {
            echo "Pipeline FAILED ❌"
        }
        always {
            echo "Cleaning up workspace files..."
            sh 'ls'
        }
    }
}

