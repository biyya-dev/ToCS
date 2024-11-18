pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Run the Python code
               bat 'javac HelloWorld.java'
            }
        }
        stage('Run') {
            steps {
               bat 'java HelloWorld'
            }
        }
    }
}
