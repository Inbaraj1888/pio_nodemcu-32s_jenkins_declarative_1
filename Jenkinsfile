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
				checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '201c9913-8f60-42e0-8584-bbc7c86a7e66', url: 'https://github.com/Inbaraj1888/pio_nodemcu-32s_jenkins_declarative_1.git']]])
			}
		}
		stage('build')
		{
			steps
			{
			sh label: '', script: '''
			platformio run'''
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
	}
}
