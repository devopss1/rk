pipeline {
  agent any
//  tools {
    //  maven 'MVN_HOME'
//  }
  stages{
	stage('git checkout'){
		steps{
			echo "checkout from GIt"
			git 'https://github.com/devopss1/rk.git'
		}	
	}
	stage('build'){
		steps{	
			echo "Build in Maven"
			sh 'mvn -f pom.xml package'
		}
	}
	stage('Artifact/Nexus'){
		steps{
			echo "Upload to Nexus"
		//	nexusArtifactUploader artifacts: [[artifactId: 'hsbcweb', classifier: '', file: '/var/lib/jenkins/workspace/job2/target/hsbcweb.war', type: 'war']], credentialsId: '996a56be-6b17-4eb6-943f-1a6200419075', groupId: 'hsbc.cc', nexusUrl: '192.168.1.112:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'snapshots', version: '1.0-SNAPSHOT'
		    nexusArtifactUploader artifacts: [[artifactId: 'hsbcweb', classifier: '', file: '/var/lib/jenkins/workspace/pipe1/target/hsbcweb.war', type: 'war']], credentialsId: '996a56be-6b17-4eb6-943f-1a6200419075', groupId: 'hsbc.cc', nexusUrl: '192.168.1.112:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'snapshots', version: '1.0-SNAPSHOT'
		    
		}
	}
	stage('Deploy to pre-preod'){
		steps{
			echo "Deploy to prepared"
			sh 'cp /var/lib/jenkins/workspace/pipe1/target/hsbcweb.war /apache-tomcat-9.0.52/webapps/'
			//sh '/root/apache-tomcat-9.0.52/bin/startup.sh'
		}	
	}
	stage('Deploy to prod'){
		steps{
			echo "Deploy to prepared"
			// sh 'cp /var/lib/jenkins/workspace/job2/target/hsbcweb.war /root/apache-tomcat-9.0.52/webapps'
		}	
	}
}
  post{
        success{
            echo "notify via email on success"
        }
        failure{
            echo " notify via email on failure"
        }
    }

}
