pipeline {
	agent {
		label 'master'
	}
	environment {
		scannerHome = tool 'sonar'
	}
	stages {
		stage ('sonar') {
			node ('master') {
				withSonarQubeEnv('sonar') {
					sh 'cd php-pm'; ${scannerHome}/bin/sonar-scanner;
				}
			}
		}
	}
}
