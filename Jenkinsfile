def TAG = '${BRANCH_NAME}'
def E2E
def MTAG = '99-SNAPSHOT'

pipeline {
    agent any
	stages {
	    stage('Build'){
	    	when { 
	    		anyOf{
	    			expression{ BRANCH_NAME ==~ /^dev.*/ }
	    			branch 'master'
	    			expression { BRANCH_NAME ==~ /staging.*/ }
	    		}
	    	}
    		node{
				def customImage = docker.build("my-image:${env.BUILD_ID}")
    		}
			steps {sh("docker build -t echo .")}
		}
	}
}