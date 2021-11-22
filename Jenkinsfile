pipeline {
    node("master") {
		stage 'Checkout'
		bin "git url: 'git@github.com:architechly/Git-Jenkins-CI.git',credentialsId: 'ssh-key-private',	branch: develop"

  // The rest of your Groovy here...

		stage 'Use Git'
  // Do anything you like with your Git repo
		sh 'git add -A && git commit -m "Update code" && git push origin master'
	}
	stages {
		
		stage('Skip the build'){
			steps {
				scmSkip(deleteBuild: false, skipPattern:'.*\\[ci skip\\].*')
			}
		}
		stage('Checkout') {
			//def gitCreds = "${env.GITCRED}"
			bat "git branch: 'develop', credentialsId: 'ssh-key-private', url:'git@github.com:architechly/Git-Jenkins-CI.git'"
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