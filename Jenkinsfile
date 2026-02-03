pipeline {
    agent {
        docker {
            image 'python:3.11-slim'
        }
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh '''
                python -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                . venv/bin/activate
                python app.py
                '''
            }
        }
    }
}


pipeline {
    agent any
    stages {

        stage('Clone Repo') {
            steps {
                echo "Cloning GitHub repository"
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing Python dependencies"
                sh '''
                python3 --version
                pip3 install -r requirements.txt
                '''
            }
        }

        stage('Run Application') {
            steps {
                echo "Running Python app"
                sh 'python3 app.py'
            }
        }

        stage('Run Tests') {
            steps {
                echo "Running unit tests"
                sh 'pytest'
            }
        }
    }

    post {
        success {
            echo "✅ Build successful!"
        }
        failure {
            echo "❌ Build failed!"
        }
    }
}
