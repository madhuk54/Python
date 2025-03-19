pipeline{
    agent any
    stages{
        stage("Checkout code"){
            steps{
                git branch:'main', url: 'https://github.com/madhuk54/PythonProject.git', credentialsId: 'github-token'credentialsId: 'token'
            }
        }
        stage("Install dependencies"){
            steps{
                bat '''
                    python -m venv venv
                    call venv\\Scripts\\activate
                    python -m pip install --upgrade pip
                    pip install -r requirements.txt
                    '''
            }
        }
        stage("Run tests"){
            steps{
                bat '''
                    call venv\\Scripts\\activate
                    pytest test.py --maxfail=1 --disable-warnings
                    '''
            }
        }
        stage("Deploy"){
            steps{
                echo "Deploying application"
                bat '''
                    call venv\\Scripts\\activate
                    python add.py
                    '''
            }
        }

    }
    post{
        success{
            echo "pipeline executed successfully"
        }
        failure{
            echo "pipelime execution failed"
        }
    }
}