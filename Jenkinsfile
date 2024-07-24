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
                git url: 'https://github.com/cosminpopovici14/jenkins.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd jenkins
                pip install -r requirements.txt
                '''
            }
        }
        stage('Build GTest') {
            steps {
                echo "Building GTest.."
                sh '''
                cd jenkins/tests/gtest
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
                cd jenkins/tests/gtest/build
                ./runTests
                '''
            }
        }
        stage('Run Script') {
            steps {
                echo "Running Script.."
                sh '''
                cd jenkins
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
