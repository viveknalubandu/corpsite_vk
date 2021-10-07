def artifactName = "ppm-jar" // also used for nexus filePath and artifactId attributes
def artifactVersion = "2.${env.BUILD_NUMBER}"
def artifactSemVersion = "${artifactVersion}.0"
def repoName = "ppm-repo"
pipeline {
    agent any
    tools { 
        maven 'Maven' 
    }
    stages {
        stage('CI') {
            steps {
			  //snDevOpsStep()
			 // error("Force fail")
			  echo 'running CI'
             sh 'mvn compile'
             sh 'mvn verify'
        	}
           post {
                always {
                    junit '**/target/surefire-reports/*.xml' 
                }
           }
        }
        stage('UAT deploy') {
            steps {
                //snDevOpsStep()
				echo 'running UAT deploy'
                sh 'mvn package'
				//snDevOpsArtifact(artifactsPayload:"""{"artifacts": [{"name": "${artifactName}","version":"${artifactVersion}","semanticVersion": "${artifactSemVersion}","repositoryName": "${repoName}"}]}""")
	    	}
        }
        stage('UAT test') {
          	steps {
				//snDevOpsStep()
                echo 'running UAT deploy'
				snDevOpsChange()
			}
        }
	}
}