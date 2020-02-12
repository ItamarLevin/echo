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
						TAG="slipperymuffin/echo:1.0.$BUILD_NUMBER"
                    } 
                    if (env.BRANCH_NAME ==~ /^dev.*/) {
                        TAG="slipperymuffin/echo:dev-$GIT_COMMIT"
                    }
                    if (env.BRANCH_NAME ==~ /^staging.*/) {
                        TAG="slipperymuffin/echo:staging-$GIT_COMMIT"
                    } 
                    sh("echo building image: ${TAG} ....")
                    sh("docker build -t ${TAG} .")
				}
			}
		}
		stage("Test"){
			steps{
				sh("echo running tests..")
			}
		}
		stage('Push'){
	    	when { 
	    		anyOf{
	    			expression{ BRANCH_NAME ==~ /^dev.*/ }
	    			branch 'master'
	    			expression { BRANCH_NAME ==~ /^staging.*/ }
	    		}
	    	}
	    	steps{
	    		sh("docker push ${TAG}")
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