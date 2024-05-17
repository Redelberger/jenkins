pipeline {
    agent any
    parameters{
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanPatram(name: 'executeTests', defauultValue: true, description: '')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the application..'
            }
        }
        stage('Test') {
            when{
                expression {
                    params.executeTests
                }
            }
            steps {
                echo 'Testing the application..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application..'
                echo "Deploying version ${params.VERSIOM}.."
            }
        }
    }
}
