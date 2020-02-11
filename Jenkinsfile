def TAG = '${BRANCH_NAME}'
def E2E
def MTAG = '99-SNAPSHOT'

pipeline {
    agent any
    tools {
        docker 'docker'
    }
	stages {
	    stage('Build'){
	    	when { 
	    		anyOf{
	    			expression{ BRANCH_NAME ==~ /^dev.*/ }
	    			branch 'master'
	    			expression { BRANCH_NAME ==~ /staging.*/ }
	    		}
	    	}
			steps {sh("docker build -t echo .")}
		}
	}
}