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
					bat "rm test2.txt"
					bat "git status"
					bat "git config --global user.email 'hari.pk@hotmail.com'"
					bat "git config --global user.name 'hariprasad'"
					//bat "git credentialsId: 'ssh-key-private', url: 'https://github.com/architechly/Git-Jenkins-CI'"
					bat "echo. 2>test2.txt"
					bat "git add ."
					bat "git commit -m 'cid'"
					bat "git push --set-upstream origin develop"
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