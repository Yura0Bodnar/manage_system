pipeline {
    agent any

    environment {
        VENV_DIR = ".venv"
        PYTHON_BIN = "python3"
    }

    stages {

        stage('Setup Python Environment') {
            steps {
                script {
                    if (!fileExists("${VENV_DIR}")) {
                        sh '${PYTHON_BIN} -m venv ${VENV_DIR}'
                    }
                    sh '''
                        source .venv/bin/activate
                        pip install --upgrade pip
                        pip install -r requirements.txt
                    '''
                }
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    source .venv/bin/activate
                    python manage.py test apps.manager
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed!'
        }
        failure {
            echo 'Tests failed. Check logs.'
        }
    }
}
