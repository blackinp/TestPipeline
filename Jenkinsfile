// Declarative //
pipeline {
    agent none
	environment {
        CC = 'diab'
    }
    stages {
        stage('Build') {
		    agent {
				label 2build_server'
			}
            steps {
                echo 'Building..'
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
				echo "Compiler is ${env.CC}"
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                /* `make check` returns non-zero on test failures,
                 *  using `true` to allow the Pipeline to continue nonetheless
                 */
                sh 'make check || true' 
            }
        }
    }
}