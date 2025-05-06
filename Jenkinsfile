pipeline {
    agent { label 'maven' }

    stages {
        stage('Git Checkout') {
            steps {
                echo 'Git checkout...'
                echo 'Repository already checked out by Jenkins.'
                sh 'ls -l' // Check the contents of the workspace
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Run') {
            steps {
                echo 'Running the application...'
                sh 'java -jar simple-java-app/target/simple-java-app-1.0.jar'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Committing and pushing the artifact to Git...'
                sh 'git config user.name "Jenkins"'
                sh 'git config user.email "jenkins@example.com"'
                sh 'git add target/simple-java-app-1.0.jar'  // Add the artifact
                sh 'git commit -m "Add built JAR artifact"'  // Commit the artifact
                sh 'git push origin master'  // Push to the master branch
            }
        }
    }
}

