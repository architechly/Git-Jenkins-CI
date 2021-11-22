pipeline {
	agent any
	environment {
		gitCredentialId = 'ssh-key-private' //defined in credentials area
		gitUrl = 'git@github.com:architechly/Git-Jenkins-CI.git'
		deployBranch = 'develop'
	}
	stages {
		
		stage('Skip the build'){
			steps {
				scmSkip(deleteBuild: false, skipPattern:'.*\\[ci skip\\].*')
			}
		}
		stage('Checkout') {
			steps {
				script{
			//def gitCreds = "${env.GITCRED}"
					bat "git branch: deployBranch, credentialsId: gitCredentialId, url:gitUrl"
				}
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
					def gitCreds = "${env.GITCRED}"
					//bat "ssh-agent (credentials : ["${gitCreds}"])"
					//bat "git status"
					bat "git status"
					bat "git credentialsId: 'ssh-key-private', url: 'https://github.com/architechly/Git-Jenkins-CI'"
					bat "git add ."
					bat "git commit -m 'ci skip Upversion Build'"
					bat "git push"
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