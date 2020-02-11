def TAG

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
						TAG="gcr.io/echo-267909/echo:1.0.$BUILD_NUMBER"
                    } 
                    if (env.BRANCH_NAME ==~ /^dev.*/) {
                        TAG="gcr.io/echo-267909/echo:dev-$GIT_COMMIT"
                    }
                    if (env.BRANCH_NAME ==~ /^staging.*/) {
                        TAG="gcr.io/echo-267909/echo:staging-$GIT_COMMIT"
                    } 
                    sh("echo building image: ${TAG}")
                    sh("docker build -t ${TAG} .")
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