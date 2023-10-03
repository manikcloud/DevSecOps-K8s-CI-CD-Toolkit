pipeline {
  agent any
  tools { 
        maven 'my_mvn'  
    }

  //  stages{
  //   stage('CompileandRunSonarAnalysis') {
  //           steps {	
	// 	sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=manikdevsecops -Dsonar.organization=manikdevsecops -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=214d1bce94b796db1450b1dd7cc017162ca38e0b'
	// 		}
  //   }

	// stage('RunSCAAnalysisUsingSnyk') {
  //           steps {		
	// 			withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
	// 				sh 'mvn snyk:test -fn'
	// 			}
	// 		}
  //   }		
	stage('Build') { 
            steps { 
               withDockerRegistry([credentialsId: "dockerHub", url: ""]) {
                 script{
                 app =  docker.build("devsecops")
                 }
               }
            }
    }

	stage('Push') {
            steps {
                script{
                    docker.withRegistry('docker tag devsecops:latest 823711539498.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:aws-credentials') {
                    app.push("latest")
                    }
                }
            }
    	}    
  }
}

