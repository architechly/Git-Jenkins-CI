pipeline {
    agent any 
	stages {
		
		stage('Skip the build'){
			steps {
				scmSkip(deleteBuild: false, skipPattern:'.*\\[ci skip\\].*')
			}
		}
        stage('Static Analysis') {
            steps {
                echo 'Run the static analysis to the code' 
            }
        }
        stage('Compile') {
            steps {
                echo 'Compile the source code' 
            }
        }
        stage('Security Check') {
            steps {
                echo 'Run the security check against the application' 
            }
        }
        stage('Run Unit Tests') {
            steps {
                echo 'Run unit tests from the source code' 
            }
        }
        stage('Run Integration Tests') {
            steps {
				script{
					echo 'Run only crucial integration tests from the source code' 
					bat "git status"
					bat "touch test.txt"
					bat "git add ."
					//bat "git commit -m '[ci skip]'
				}
                
            }
        }
        stage('Publish Artifacts') {
            steps {
                script {
					echo 'Save the assemblies generated from the compilation' 
					def gitCreds = "${env.GITCRED}"
					sshagent (credentials : ["${gitCreds}"]) {
						sh "git commit -m '[ci skip] Upversion Build'"
						sh "git push"
					}
				}
            }
        }
			
    }
	
}