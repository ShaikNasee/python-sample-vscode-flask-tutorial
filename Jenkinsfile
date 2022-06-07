pipeline{
    agent{ label 'python_build' }
    stages{
        stage( 'source code from git' ){
            steps{
              git branch : 'master' url: 'https://github.com/ShaikNasee/python-sample-vscode-flask-tutorial.git'
            }
        }
        stage('build'){
            steps{
                sh 'pip install -r requirements.txt'
            }
        }
        stage('test'){
            steps{
                sh ' pip install pytest pytest-azurepipelines '
                sh ' pip install pytest-cov '
                sh ' /home/python/.local/bin/pytest --doctest-modules --junitxml=junit/test-results.xml --cov=. --cov-report=xml'
            }
        }
        stage( 'publish'){
            steps{
                junit testResults: '**/test-*.xml'
            }
        }
    }
}