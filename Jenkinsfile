pipeline{
    agent{ label 'build_pipeline' }
    triggers{ cron '0 * * * *'}
    stages{
        stage( 'checkout' ){
            steps{
                git url: 'https://github.com/ashishdevops123/python.git',
                    branch: 'master'
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
                sh ' /home/jenkins/.local/bin/pytest --doctest-modules --junitxml=junit/test-results.xml --cov=. --cov-report=xml'
            }
        }
        stage( 'publish'){
            steps{
                junit testResults: '**/test-*.xml'
            }
        }
    }
}