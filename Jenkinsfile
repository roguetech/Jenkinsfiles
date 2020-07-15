def NODE_LABEL = 'master'
def SCM_URL = 'git@' + env.GITLAB_SERVER + ':configuration/aws-functions.git'
def SCM_VARS = null
def SCM_IDENIFIER = '0f462594-06c0-49ca-bba3-210135a8cc89'

node('master') {

}

pipeline {
    agent none

    options {
        disableConcurrentBuilds()
        skipDefaultCheckout false
        timeout(time: 60, unit: 'MINUTES')
    }

    environment {
        BRANCH_NAME = null
    }

    parameters {
        choice(name: 'GIT_BRANCH', choices: ['master', ''], description: 'The branch to checkout for non shared qa specific code')
    }

    stages {
        stage('Run') {
            steps {
                sh "echo \"Hello World\""
            }
        }
    }

    post {
        failure {
            echo "failed"
        }
        success {
            echo "success"
            build job: 'test'
        }
        always {
            node(NODE_LABEL) {
                cleanWs()
            }
        }
    }
  }
