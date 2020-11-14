pipeline {
    agent any
    stages {
        stage('opdracht 5') {
            steps {
                echo "good luck..."
            }
        }
	stage('checkout code'){
	sleep (30)
	sshagent(credentials : ['Github']){
	sh "scp -o StrictHostKeyChecking=no CurrentBuild.zip ubuntu@instanceInfo$remotedir"
	sh "ssh -T -o StrictHostKeyChecking=no ubuntu@instanceInfo sudo unzip CurrentBuild.zip -d /var/www/html"
	}
        }
    }
}
