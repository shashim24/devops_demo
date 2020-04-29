pipeline {
	agent any

	stages {
		stage('Build') {
			steps {
				echo 'Building...'
				echo "Running ${env.BUILD_ID} ${env.BUILD_DISPLAY_NAME} on ${env.NODE_NAME} and JOB ${env.JOB_NAME}"
				bat """
					cd java_web_code
					mvn install
				"""			
			}
		}
		stage('Test') {
			steps {
				echo 'Testing...'
				bat """
					cd ..\\integration-testing\\
					mvn clean verify -P integration-test
				"""	
			}
		}
		stage('Deploy') {
			steps {
				echo 'Deploying...'
				bat """
					cd java_web_code\\
					\\bin\\cp target\\wildfly-spring-boot-sample-1.0.0.war ..\\docker\\
					cd ..\\docker\\
					docker build -t devops_pipeline_demo .
					docker run -d -p 8180:8080 --name devops_pipeline_demo devops_pipeline_demo
				"""

				echo "--------------------------------------------------------"
				echo "View App deployed here: http://server-ip:8180/sample.txt"
				echo "--------------------------------------------------------"
			}
		}
  	}
}
