node {
    def jupyterUG4

    stage('Clone repository') {
        checkout scm
        sh 'cat /etc/os-release'
        sh 'docker version' 
    }

    stage('Build image') {
       jupyterUG4 = docker.build("modsim")
    }

    stage('Test image') {
        jupyterUG4.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'git') {
            jupyterUG4.push("${env.BUILD_NUMBER}")
            jupyterUG4.push("latest")
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

