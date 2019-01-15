pipeline {
	agent any
	
	stages {
		stage('checkout') {
			steps {				
				checkout([
					$class: 'GitSCM',
					branches: scm.branches,
					extensions: scm.extensions,
					userRemoteConfigs: scm.userRemoteConfigs])

				echo "Retrieved $env.BRANCH_NAME in workspace: $env.WORKSPACE"
			}
		}
		
		stage('build') {
			steps {
				bat "\"${tool 'msBuildTest'}\\msbuild.exe\" \"$env.WORKSPACE\\SetupCI\\SetupCI.sln\" /t:restore;build /p:RestoreSources=\"https://api.nuget.org/v3/index.json\" /p:Configuration=Release /p:Platform=\"Any CPU\""
			}
		}
	}
}