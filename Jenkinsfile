pipeline {
	agent any
	stages {
		stage('Setup') {
			script {
				LATEST_COMMIT = sh (script: "git log -n 1 --pretty=format:'%H'", returnStdout: true)
			}
		}
		stage('Build') {
			steps {
				sh 'mvn package -Drat.skip=true'
			}
		}
	}
	post {
		failure {
			sh "git bisect start ${LATEST_COMMIT} f12518c4d471c30d33a4d16126adbc7e6d563188"
				sh "git bisect run mvn clean test -Drat.skip=true"
				sh "git bisect reset"
		}
	}
}