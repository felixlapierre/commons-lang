pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
				sh 'mvn package -Drat.skip=true'
			}
		}
	}
	post {
		failure {
			sh "git bisect start ${BROKEN} ${STABLE}"
				sh "git bisect run mvn clean test -Drat.skip=true"
				sh "git bisect reset"
		}
	}
}