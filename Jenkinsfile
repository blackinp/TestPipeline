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
				echo "Compiler is on ${env.CC}"
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
        stage('Deploy') {
            when {
                expression {
                    /* 如果测试失败，状态为UNSTABLE */
                    currentBuild.result == null || currentBuild.result == 'SUCCESS' 
                }
            }
            steps {
                echo 'Deploying..'
                sh 'make publish'
            }
        }
    }
}