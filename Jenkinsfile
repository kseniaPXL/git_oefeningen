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
		sh 'sudo visudo'    
		sh 'composer install'
		sh 'sudo apt-get update'
		sh 'sudo apt-get install apache2'
		sh 'sudo add-apt-repository ppa:ondrej/php'
		sh 'sudo apt-get update'
		sh 'sudo apt-get -y install php7.3 php7.3-xml php7.3-mbstring'   
		sh 'sudo curl -s https://getcomposer.org/installer | php'
		sh 'sudo mv composer.phar /usr/local/bin/composer'  
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
    }
}
