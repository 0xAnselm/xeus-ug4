pipeline {
    agent any
        // Mods including submodule behaviour 
    environment {
        DEV_BRANCH="main"
        STABLE_BRANCH="stable"
    }
    stages {
        stage('Checkout main repo') {
            steps {
                node {
					checkout scm
					def testImage = docker.build("modsim", "./docker/Dockerfile") 

					testImage.inside {
						echo 'Place test here'
					}
				}
            }
        }
    }
    post { 
        always { 
            echo 'I will always clean'
            cleanWs()
            dir("${env.WORKSPACE}@tmp") {
                deleteDir()
            }
        }
        success {
            echo 'Yippiiiieeee - Dockerfile build success'
        }
        failure {
            echo ':( - Work on your Dockerfile'
        }
    }
}

