def gv

pipeline {
    agent {
        label 'docker-agent-alpine'
    }
    parameters{
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    stages {
        stage('Init') {
            steps {
                echo 'Loading main script..'
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    gv.buildApp()
                }
            }
        }
        stage('Test') {
            when{
                expression {
                    params.executeTests
                }
            }
            steps {
                script {
                    gv.testApp()
                }
            }
        }
        stage('Deploy') {
            steps {
                timeout(time: 15, unit: "MINUTES") {
	                input id: 'Approved', message: 'Has the previous been approved so we can proceed?', ok: 'Approved?', submitter: 'tobias@redelberger.onmicrosoft.com,012d1367-f5d3-4fbe-9697-b3d1e083daec', submitterParameter: 'Approver'
	            }
                script {
                    gv.deployApp()
                }
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}