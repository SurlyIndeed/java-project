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
		sh 'aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://jenkins-s3bucket-f0wrdpg4floe'   
	}   
	stage('Report') {    
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'cfcf6c63-081f-4359-84d3-900c49b2a975', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
		sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
		}
	}   
}