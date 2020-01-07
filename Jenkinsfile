pipeline {
	agent any
	stages {
		stage('Source') { 
			steps {
				checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/prabhavagrawal/discoveri-happytrip.git']]])
			}
		}
		stage('Build') { 
			tools {
				jdk 'jdk8'
				maven 'apache-maven-3.5.4'
			}
			steps {
				powershell 'java -version'
				powershell 'mvn -version'
				powershell 'mvn clean package'
				archiveArtifacts 'target/*.war'

			}
		}
		
		stage('Deploy To Prod'){
			input{
				message "Do you want to proceed for Production Deployment?"
			}
			steps{
				sh 'echo "Deploy into Prod"'
			}
		}
    		stage('test') {
            		steps{
                		powershell(script:'Write-Output Hello')
            		}
        	}
		stage('Deploy') {
			steps{
				echo 'deployed'
				deploy adapters: [tomcat7(credentialsId: 'e0cdb588-e5bc-45d6-9bfb-0c0dfae96362', url: 'http://localhost:8085')], contextPath: 'happytrip', war: '**/*.war'
			}
		}
	}
}
