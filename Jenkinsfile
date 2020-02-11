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
	    			expression { BRANCH_NAME ==~ /^staging.*/ }
	    		}
	    	}
    		
			steps {
				script{
					if (env.BRANCH_NAME == 'master') {
                        sh("docker build -t master .")
                    } 
                    if (env.BRANCH_NAME ==~ /^dev.*/) {
                        sh("docker build -t dev .")
                    }
                    if (env.BRANCH_NAME ==~ /^staging.*/) {
                        sh("docker build -t stage .")
                    } 
                    echo sh("echo $BRANCH_NAME is the branch")
				}
			}
		}
	}
}