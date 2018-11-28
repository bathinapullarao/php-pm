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
					sh '${scannerHome}/bin/sonar-scanner'
				}
			}
			}
		}
		
		stage ('Static code analysis') {
			steps{
				node('master'){
                      sh "sudo phpcs --config-set ignore_warnings_on_exit 1 --report=checkstyle --report-file=checkstyle-result.xml -q /code"
                      step([$class: 'hudson.plugins.checkstyle.CheckStylePublisher', pattern: 'checkstyle-*'])
                 
				}}}
		
		
		stage ('sleep') {
			steps {
				node ('master') {
					sleep 100 
				}
			}
		}
		stage (sonarstatus) {
			steps {
				script {
					def qualitygate = waitForQualityGate()
					if (qualitygate.status != "OK") {
						echo "Quality gate is fail"
	}
					else {
						echo "Quality Gate has pass"
					}
				}
			}
		}
}
}
