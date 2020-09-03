pipeline {
    agent any
	parameters {
				string(name: 'VersionLabel', defaultValue: 'v1', description: 'Enter Version label')
	}
	stages{
        stage('Push to S3') {
            steps {
                sh 'aws s3 cp ebdemo.war s3://elasticbeanstalk-eu-west-2-732799771072'
            }
       }
	   stage('create version') {
            steps {
                sh 'aws elasticbeanstalk create-application-version --application-name Jenkins-eb-test --version-label v1 --description MyAppv1 --source-bundle S3Bucket="elasticbeanstalk-eu-west-2-732799771072",S3Key="ebdemo.war" --region="eu-west-2"'
            }
       }
	   stage('Deploy version') {
            steps {
                sh 'aws elasticbeanstalk update-environment --environment-name JenkinsEbTest-env --version-label v1 --region="eu-west-2"'
            }
       }
	}
}