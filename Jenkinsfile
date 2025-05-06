pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                echo 'Git checkout...'
                echo 'Repository already checked out by Jenkins.'
                sh 'ls -l' // Check the contents of the workspace
            }
        }

        stage('Build') {
            agent { label 'maven' }
            steps {
                echo 'Building the project...'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo "No tests in this project"'
            }
        }

        stage('Run') {
            steps {
                echo 'Running the application...'
                sh 'java -cp target/simple-java-app-1.0.jar com.example.HelloWorld'
            }
        }
    }
}

