pipeline {
    agent { label 'maven' }

    stages {
        stage('Git Checkout') {
          steps {
              echo 'Git checkout...'
              checkout([$class: 'GitSCM',
                  branches: [[name: '*/master']],
                  userRemoteConfigs: [[url: 'https://github.com/kiran97patil/simple-java-app.git', credentialsId: 'github-creadential']]
              ])
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
                sh '''
                    git config user.name "Jenkins"
                    git config user.email "jenkins@example.com"

                    git add target/simple-java-app-1.0.jar || true

                    # Only commit if there are changes
                    if ! git diff --cached --quiet; then
                        git commit -m "Add built JAR artifact"
                        git push origin master
                    else
                        echo "No changes to commit."
                    fi
                '''
            }
        }
    }
}

