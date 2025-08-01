pipeline {
    agent { 
        node {
            label  'docker-agent-python_dockercli' 
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
                echo "Doing build stuff on Docker agent.."
                '''
            }
        }
        
        stage('Test') {
            steps {
                echo "Testing.. This is the second stage of the pipeline."
                sh '''
                cd myapp
                . venv/bin/activate
                python3 hello.py
                python3 hello.py --name=Shaikh
                echo "Tests completed successfully."
                '''
            }
        }
        
        stage('Docker Build and Run') {
            steps {
                echo 'Building Docker image and running container...'
                sh '''
                cd myapp
                docker build -t myapp-image .
                docker rm -f myapp-container || true
                docker run -d --name myapp-container myapp-image
                '''
            }
        }
    }
    
    post {
        always {
            echo 'Cleaning up Docker container and image...'
            sh '''
            docker rm -f myapp-container || true
            docker rmi -f myapp-image || true
            '''
        }
    }
}
