pipeline {
    agent any
    stages {
        stage('opdracht 5') {
            steps {
                echo "good luck..."
            }
        }
	    
	stage('checkout code') {
            steps {
                git 'https://github.com/d-ries/2TIN-DevOps-Calculator'
                echo 'code is opgehaald'
            }
        }
	stage('install dependencies') {
	    steps {
		echo 'installing dependencies'
		    sh ' pwd > waar.txt'
		    sh ' cat waar.txt'
		    
		//sh 'sudo visudo'    
		sh 'composer install'
		//sh 'sudo apt-get update'
		    //sh 'echo $PASSWORD"
		//sh 'sudo apt-get install apache2'
		//sh 'sudo add-apt-repository ppa:ondrej/php'
		//sh 'sudo apt-get update'
		//sh 'sudo apt-get -y install php7.3 php7.3-xml php7.3-mbstring'   
		sh 'sudo curl -s https://getcomposer.org/installer | php'
		//sh 'sudo mv composer.phar /var/lib/jenkins/workspace/composer'  
	    }
	}
	stage('unittest') {
	    steps {
		echo 'Running unit tests'
		sh './vendor/bin/phpunit tests'   
		echo 'Building a JUnit report'
		junit allowEmptyResults: true, testResults: '**/test-results/*.xml'
	    }
	}
   stage('create bundle') {
	    steps {
		 echo 'making the bundle and zipping the file'
    		 sh 'mkdir bundle'
		 sh 'zip -r bundle.zip composer.json docker-compose.yml dockerfile index.php tests src assets'
		 sh 'mv bundle.zip bundle'
	    }
	}
	   
    }
	 post {
		    success {
			   archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
            		   junit 'build/reports/**/*.xml'
		    }
		    failure {
            		    sh 'cat build is gefaald > error.txt'
			    //sh 'mv error.txt /home/jenkins'
        			}
	    }
	}

