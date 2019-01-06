// Declarative //
pipeline {
    agent any
	environment {
        CC = 'diab'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
				echo "Compiler is on ${env.CC}"            }
			post {
			always {
				echo 'post always'
			}
			success {
				echo 'post success'
			}
			failure {
				echo 'post failure'
			}
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
			post {
			always {
				echo 'post always'
			}
			success {
				echo 'post success'
			}
			failure {
				echo 'post failure'
			}
        }

    }
}