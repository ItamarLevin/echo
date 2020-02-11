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
                        sh("docker build -t gcr.io/echo-267909/echo:1.0.$BUILD_NUMBER .")
                    } 
                    if (env.BRANCH_NAME ==~ /^dev.*/) {
                        sh("docker build -t gcr.io/echo-267909/echo:dev-$GIT_COMMIT .")
                    }
                    if (env.BRANCH_NAME ==~ /^staging.*/) {
                        sh("docker build -t gcr.io/echo-267909/echo:staging-$GIT_COMMIT .")
                    } 
                    echo sh("echo $BRANCH_NAME is the branch")
				}
			}
		}
	}
	post { 
        always { 
            echo 'delete unused images...'
            sh("docker image prune -af")
        }
    }
}