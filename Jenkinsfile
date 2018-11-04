pipeline {
	agent {
		label 'master'
	}
	environment {
		scannerHome = tool 'sonar'
	}
	stages {
		stage ('checkout') {
			steps {
				node ('master') {
					checkout scm
				}
			}
		}
		stage ('sonar') {
			steps {
			node ('master') {
				withSonarQubeEnv('sonar') {
					sh 'cd php-pm; ${scannerHome}/bin/sonar-scanner'
				}
			}
			}
		}
	}
}
