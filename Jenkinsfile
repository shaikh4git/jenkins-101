pipeline {
    agent { 
        node {
            label 'docker-agent-python'
            }
      }
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.. This is the first stage of the pipeline."
                sh '''
                cd myapp
                python3 -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt
                echo "Installed all the requirements for the Python app."
                echo "doing build stuff on Docker agent.."
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.. This is the second stage of the pipeline."
                sh '''
                cd myapp
                python3 hello.py
                python3 hello.py --name=Shaikh
                echo "Tests completed successfully."
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.. This is gonna be the 4th build."
                '''
            }
        }
    }
}