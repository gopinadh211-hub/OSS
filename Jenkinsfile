pipeline {
    agent any
  tools {
    maven 'maven3'
	}
	stages{
	    stage('Build') {
		  steps{
		      sh 'mvn clean package'
      }
      }
	  stage('sonarqube analysis') {
		     steps{
			      withsonarqubeenv('sonarqube') {
				  sh "mvn sonar:sonar"
				  }
			}
		}
		stage("Quality Gate") {
		steps {
		//timeout(time:1, unit: 'HOURS') {
		//waitForQualityGate abortPipeline: true
		//}
		        echo 'test'
		}
	  }
	  stage('upload war to nexus'){
          steps{	  
	         nexusArtifactUploader artifacts: [[artifactId: 'WebApp', classifier: '', file: 'target/Maven.webapp-1.0.0.war', type: 'war']], credentialsId: 'nexus3', groupId: 'Demoapp', nexusUrl: '20.212.18.14', nexusVersion: 'nexus3', protocol: 'http', repository: 'projectoss-release', version: '1.0.0'
	  }
	  }
	  }
	  }
