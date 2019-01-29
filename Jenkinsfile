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
				bat "\"${tool 'msBuildTest'}\\msbuild.exe\" \"$env.WORKSPACE\\SetupCI\\SetupCI.sln\" /t:restore;build /p:RestoreSources=\"https://api.nuget.org/v3/index.json\" /p:RestorePackagesPath=\"C:\\TestFolderNugetCache\" /p:Configuration=Release /p:Platform=\"Any CPU\""
			}
		}
		
		stage('unit tests') {
			steps {
				bat "for /f \"delims=\" %%a in ('dir \"$env.WORKSPACE\\SetupCI.Test\" /b /s *.Test.csproj') do dotnet test \"%%a\" --configuration Release --no-build --no-restore --logger \"trx;LogFileName=..\\..\\unit_tests_results\\%%~nxa.trx\""
			}
			post{
				always{
					step([$class: 'MSTestPublisher', testResultsFile:"unit_tests_results\\*.trx", failOnError: true, keepLongStdio: true])
				}
			}
		}
	}
}