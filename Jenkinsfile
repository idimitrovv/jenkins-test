pipeline {
	agent any
	
	stages {
		stage('checkout') {
			steps {
				echo 'Hello world of Jenkins!' + scm.userRemoteConfigs
				
				checkout([
					$class: 'GitSCM',
					branches: [[name: '*/master']],
					doGenerateSubmoduleConfigurations: false,
					extensions: [],
					submoduleCfg: [],
					userRemoteConfigs: [[]]])
			}
		}
	}
}