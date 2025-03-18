pipeline {
   	 agent any

options {
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '3', numToKeepStr: '3')
  quietPeriod 15
}

environment {
  PROJECT_NAME = "demo_pipeline_banch"
}

        stages {
        	stage('Preparation') {
          		  steps {
               			 echo "Starting pipeline for project: $PROJECT_NAME"
           			 }
      		  }

        	stage('Build') {
            		when {
              		  branch 'developer'
          		 }
          		  steps {
           		     echo "Building for developer branch..."
                		// Add your build steps here
            		}
       		 }

      		stage('Test') {
     		       when {
      		          branch 'tester'
    		        }
   		         steps {
        		        echo "Running tests on tester branch..."
    	          		  // Add your test steps here
         		   }
    		 }

     		 stage('Deploy to Staging') {
           		when {
            		    branch 'staging'
         		}
          		  steps {
                		echo "Deploying to staging environment..."
              				  // Add your deployment steps here
				script {
                   			 input message: "Proceed to Production?", ok: "Deploy"
               			 }
		        }
     		  }

		    stage('Production Deployment') {
            		when {
				branch 'production'
            		}
          		  steps {
          			      echo "Deploying to production environment..."
            			    // Add your production deployment steps here
           		 }
      		  }
 	   }

			post {
       				always {
        	 		   echo "Pipeline complete for branch: $PROJECT_NAME"
       				 }
        			success {
           				 echo "Pipeline succeeded!"
     				 }
			}
}
