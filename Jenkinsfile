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
		sh 'vendor/bin/phpunit -c build/reports/**/phpunit.xml || exit 0'
		//junit 'build/reports/**/*.xml'    
		//phpunit --log-junit report.xml   
		//junit allowEmptyResults: true, testResults: '**/test-results/*.xml'
	    }
	}
   stage('create bundle') {
	    steps {
		 sh 'rm -rf bundle'
		 sh 'rm -rf bundle.zip'   
		 echo 'making the bundle and zipping the file'
    		 sh 'mkdir bundle'
		 sh 'mv composer.json bundle/' 
		 sh 'mv docker-compose.yml bundle/'  
		  sh 'mv dockerfile  bundle/' 
		 sh 'mv index.php bundle/'   
		 sh 'zip -r bundle.zip bundle'
		 //sh 'mv bundle.zip bundle'
	    }
	}
	   
    }
	 post {
		    success {
			   archiveArtifacts artifacts: 'build/libs/**/*.xml', fingerprint: true
            		   junit 'build/reports/**/*.xml'
		    }
		    failure {
            		    sh 'echo build is gefaald > error.txt'
			    //sh 'mv error.txt /home/jenkins'
        			}
	    }
	}

