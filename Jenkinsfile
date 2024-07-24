pipeline {
    agent { 
        node {
            label 'docker-agent-python'
        }
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('Pull from Git') {
            steps {
                echo "Pulling from Git..."
                git url: 'https://url-catre-repo-git.git', branch: 'branch-name'
            }
        }
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd myapp
                pip install -r requirements.txt
                '''
            }
        }
        stage('Build GTest') {
            steps {
                echo "Building GTest.."
                sh '''
                cd myapp/tests/gtest
                mkdir -p build
                cd build
                cmake ..
                make
                '''
            }
        }
        stage('Run GTest') {
            steps {
                echo "Running GTest.."
                sh '''
                cd myapp/tests/gtest/build
                ./runTests
                '''
            }
        }
        stage('Run Script') {
            steps {
                echo "Running Script.."
                sh '''
                cd myapp
                python3 test.py
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
            // Orice pas de curățenie care trebuie executat indiferent de succesul pipeline-ului
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
