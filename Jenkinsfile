pipeline{
	agent any
	environment {
		LANG='en_US.UTF-8'
		LC_ALL='en_US.UTF-8'
	}
	tools{
		maven 'Maven'
	}
	
	stages {
		stage('Checkout'){
			steps{
				git branch : 'master' , url : 'https://github.com/ThisisRishavKumar/webapp.git'
			}
		}
		
		stage('Build') {
			steps {
				sh 'mvn clean install'
			}
		}
		
		stage('Archieve') {
			steps{
				archiveArtifacts artifacts : 'target/*.war', fingerprint:true
			}
		}
		stage('Deploy'){
			steps{
				sh 'mvn clean package'
				sh 'ansible-playbook ansible/playbook.yml -i ansible/host.ini'
			}
		}
	}
	post{
		success {
			echo 'Deployed Successfully'
		}
		
		failure {
			echo 'Deployment Failed'
		}
	}
}
		
