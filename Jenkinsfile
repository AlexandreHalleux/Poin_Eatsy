pipeline {
    agent any

    stages {
        stage('Package') {
			steps {
				echo 'Package...'
                bat 'mvn clean package'
            }
        }
		stage('Analyse') {
			steps {
				echo 'Analyse...'
			}
        }
    }
	post{
		always{
			archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            junit '/**/*.xml'

		    recordIssues enabledForFailure: true, tools: [mavenConsole(), java()]
			recordIssues enabledForFailure: true, tools: checkStyle()
			recordIssues enabledForFailure: true, tools: spotBugs()
			recordIssues enabledForFailure: true, tools: cpd(pattern: '**/target/cpd.xml')
			recordIssues enabledForFailure: true, tools: pmdParser(pattern: '**/target/pmd.xml')
		}
	}
}