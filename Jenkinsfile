@Library('jenkins-library@master') _

pipeline
{
	agent any
	stages
	{
		stage('Checkout')
		{
			steps
			{
				cleanWs()
				checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Github_Credentials', url: 'https://github.com/Inbaraj1888/pio_nodemcu-32s_jenkins_declarative_1.git']]])
				
			}
		}
		stage('Building')
		{
			steps
			{
				
			sh label: '', script: '''
			platformio run'''
			fileOperations([fileZipOperation('.pio')])
			}

		}
		stage('test')
		{
			steps
			{
			sh label: '', script: '''
			platformio test -e nodemcu-32s --verbose'''
			}
		}
		stage('Flash')
		{
			steps
			{
			sh label: '', script: '''
			platformio run -t upload'''
			}
		}
		stage('Upload')
		{
			steps
			{
			rtUpload (
				serverId: 'jenkins-artifactory-server',
				spec: '''{
					"files": [
						{
						"pattern": "${WORKSPACE}/.pio.zip",
						"target": "libs-release-local"
						}
					]
					}'''
				)
			}
		}
		
		
	}
}
