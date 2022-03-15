pipeline {
  agent any
  stages {
    stage("Build Application"){
    	steps{
    		bat 'mvn clean install'
    	}
    }
    stage("Perfrom MUnit Test"){
    	steps{
    		bat 'mvn test'
    	}
    }
    stage("Deploy Application To Cloudhub"){
    	steps{
    		bat 'mvn package deploy -DmuleDeply'
    	}
    }
    stage("Perform Regression Test"){
      steps {
        script {
			bat 'npm install'
			try{
				bat 'npm run app-tests-prod'
				currentBuild.result = 'SUCCESS'
			} catch(Exception e){
				currentBuild.result = 'FAILURE'
			}
            junit 'newman.xml'
        }
      }
    }    
  }
}