pipeline{
  agent any
  stages{
    stage('docker build'){
	    steps {	    
	      sh 'echo ${BUILD_NUMBER}'
	      sh "docker build --no-cache -t kapilgupta15n/frontend:${BUILD_NUMBER} ."
	    }
	  }
	  stage ('docker push') {
	    steps {
	      withCredentials([usernamePassword(credentialsId: 'fe190092-0b08-4f1d-9633-37df4a80057e', passwordVariable: 'Password', usernameVariable: 'Username')]) {
         sh "docker login -u ${env.Username} -p ${env.Password}"
	       sh "docker push kapilgupta15n/frontend:${env.BUILD_NUMBER}" 
	      }
	    }
    }
	  stage ('Launch Container') {
	    steps{
	      sh "docker run -d --restart=always -p 80:80 kapilgupta15n/frontend:${env.BUILD_NUMBER}"
	    }
	  }
  }	
  post {
    always {
      deleteDir() /* cleanup the workspace */
    }
  }
}
