pipeline {
    agent { 
        docker {
            label 'docker-agent-python'
            image 'devopsjourney1/myjenkinsagents:python'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
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
                echo "Building Python dependencies..."
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Build GTest') {
            steps {
                echo "Building GTest..."
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
                echo "Running GTest..."
                sh '''
                cd jenkins/tests/gtest/build
                ./runTests
                '''
            }
        }
        stage('Run Script') {
            steps {
                echo "Running Python script..."
                sh 'python3 test.py'
            }
        }
        stage('Deliver') {
            steps {
                echo 'Delivering...'
                sh 'echo "Doing delivery stuff..."'
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
