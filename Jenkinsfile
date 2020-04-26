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
		cd java_web_code/
		cd ../docker/
		docker build -t devops_pipeline_demo .
		CONTAINER=devops_pipeline_demo
 
		RUNNING=$(docker inspect --format="{{ .State.Running }}" $CONTAINER 2> /dev/null)

		if [ $? -eq 1 ]; then
		  echo "'$CONTAINER' does not exist."
		else
		  docker rm -f $CONTAINER
		fi

		echo ""
		echo "..... Deployment Phase Started :: Building Docker Container :: ......"
		docker run -d -p 8180:8080 --name devops_pipeline_demo devops_pipeline_demo

		echo "--------------------------------------------------------"
		echo "View App deployed here: http://server-ip:8180/sample.txt"
		echo "--------------------------------------------------------"
     }
   }
  }
}
