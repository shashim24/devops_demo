pipeline {
   agent any

   stages {
		stage('Build') {
			steps {
				echo 'Building...'
				echo "Running ${env.BUILD_ID} ${env.BUILD_DISPLAY_NAME} on ${env.NODE_NAME} and JOB ${env.JOB_NAME}"
				sh 'cd java_web_code'
				sh 'mvn install'
			}
		}
		stage('Test') {
			steps {
				echo 'Testing...'
			}
		}
		stage('Deploy') {
			steps {
				echo 'Deploying...'	
			}
		}
	}
}
