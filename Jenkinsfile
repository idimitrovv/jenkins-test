pipeline {
	agent any
	
	stages {
		stage('checkout') {
			steps {
				echo 'Hello world of Jenkins!'
				
				checkout([
					$class: 'GitSCM',
					branches: scm.branches,
					extensions: scm.extensions,
					userRemoteConfigs: scm.userRemoteConfigs])

			}
		}
	}
}