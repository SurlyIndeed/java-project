properties([pipelineTriggers([githubPush()])])
node('linux') {   
	stage('Unit Tests') {    
		git 'https://github.com/SurlyIndeed/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'   
   
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
	stage('Deploy') {    
		sh 'aws S3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://jenkins-s3bucket-f0wrdpg4floe'   
	}   
}