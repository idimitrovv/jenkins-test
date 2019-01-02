pipeline {
	agent any
	
	stages {
		stage('checkout') {
			steps {
				echo 'Hello world of Jenkins!'
				
				checkout([
					$class: 'GitSCM',
					branches: [[name: '*/master']],
					doGenerateSubmoduleConfigurations: false,
					extensions: [],
					submoduleCfg: [],
					userRemoteConfigs: [[url: 'https://github.com/idimitrovv/jenkins-test']]])

			}
		}
	}
}