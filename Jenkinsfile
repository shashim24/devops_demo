pipeline {
   agent any

   stages {
      stage('Build') {
        steps {
          echo 'Building...'
          echo "Running ${env.BUILD_ID} ${env.BUILD_DISPLAY_NAME} on ${env.NODE_NAME} and JOB ${env.JOB_NAME}"
		  cd java_web_code
		  mvn install
        }
   }
   stage('Test') {
     steps {
        echo 'Testing...'
		cd ../integration-testing/
		mvn clean verify -P integration-test
     }
   }
   stage('Deploy') {
     steps {
		echo 'Deploying...'
		
     }
   }
  }
}
