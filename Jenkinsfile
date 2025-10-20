pipeline {
    agent any

    environment {
        PYTHON_HOME = 'python'
    }

    stages {
        stage('install-pip-deps') {
            steps {
                echo 'Klonējam python-greetings repozitoriju'
                bat 'if exist greetings-app (rmdir /S /Q greetings-app)'
                bat 'git clone https://github.com/mtararujs/python-greetings greetings-app'
                echo 'Parādam failus'
                bat 'dir greetings-app'
                echo 'Instalējam atkarības'
                bat 'pip install -r greetings-app\\requirements.txt'
            }
        }

        stage('deploy-to-dev') {
            steps {
                script {
                    deployApp('dev', 7001)
                }
            }
        }

        stage('tests-on-dev') {
            steps {
                script {
                    runTests('dev')
                }
            }
        }

        stage('deploy-to-staging') {
            steps {
                script {
                    deployApp('stg', 7002)
                }
            }
        }

        stage('tests-on-staging') {
            steps {
                script {
                    runTests('stg')
                }
            }
        }

        stage('deploy-to-preprod') {
            steps {
                script {
                    deployApp('preprod', 7003)
                }
            }
        }

        stage('tests-on-preprod') {
            steps {
                script {
                    runTests('preprod')
                }
            }
        }

        stage('deploy-to-prod') {
            steps {
                script {
                    deployApp('prod', 7004)
                }
            }
        }

        stage('tests-on-prod') {
            steps {
                script {
                    runTests('prod')
                }
            }
        }
    }
}

def deployApp(envName, port) {
    echo "Apstādinām ${envName} servisu"
    bat "pm2 delete greetings-app-${envName} & exit 0"

    echo "Startējam ${envName} vidi uz porta ${port}"
    bat "pm2 start greetings-app\\app.py --name greetings-app-${envName} -- --port ${port}"
}

def runTests(envName) {
    echo "Klonējam testu repozitoriju"
    bat 'if exist greetings-tests (rmdir /S /Q greetings-tests)'
    bat 'git clone https://github.com/mtararujs/course-js-api-framework greetings-tests'

    echo "Instalējam node atkarības"
    bat 'cd greetings-tests && npm install'

    echo "Palaidām testus uz greetings-${envName}"
    bat "cd greetings-tests && npm run greetings greetings_${envName}"
}
