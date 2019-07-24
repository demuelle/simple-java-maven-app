pipeline {
	agent any
	tools {
		maven 'maven'
		jdk 'jdk8'
	}
	stages {
		stage ('Initialize') {
			steps {
				sh '''
				echo "PATH = ${PATH}"
				echo "M2_HOME = ${M2_HOME}"
				'''
			}
		}
		stage('Build') {
			steps {
				sh 'mvn -B -DskipTests clean package'
			}
		}
		stage('Test') {
			steps {
				sh 'mvn test'
			}
			post {
				always {
					junit 'target/surefire-reports/*.xml'
				}
			}
		}
		stage('Deliver') {
			steps {
				sh './jenkins/scripts/deliver.sh'
			}
		}
	}
	post {
		always {
			archiveArtifacts artifacts: '**/my-app-1.0-SNAPSHOT.jar', fingerprint: true
		}
	}
}
