pipeline {
    agent any
    stages {
        stage('Clone repository~') {
            steps {
                checkout scm
            }
        }
	stage('Check Information') {
	    steps {
		sh 'pwd'
		sh 'whoami'
		sh 'ls'
		sh 'cat /etc/passwd'
		sh 'ls /home/'
		sh 'ls /var/run/'
            }
	}
	stage('Setting Docker') {
	    steps {
		sh 'docker --version'
            }
	}
        stage('Build Image~') {
            steps {
                script {
                    app = docker.build("yangsubinn/opensource-2023")
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'yangsubin') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
