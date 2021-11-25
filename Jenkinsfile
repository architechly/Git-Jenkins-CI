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
			  scmSkip(deleteBuild: false, skipPattern:'.*\\[ci-skip\\].*')
			  //echo "${currentResult.currentResult}"
			} 			
		}
		
		stage('Static Analysis') {
            steps {
				//def test= ${currentResult.currentResult}
                echo 'Run the static analysis to the code ' 
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
					//bat "rm test2.txt"
					//bat "git status"
					//bat "git config --global user.email 'hari.pk@hotmail.com'"
					//bat "git config --global user.name 'hariprasad'"
					//bat "git credentialsId: 'ssh-key-private', url: 'https://github.com/architechly/Git-Jenkins-CI'"
					//bat "echo. 2>test3.txt"
					//bat "git add ."
					//bat "git commit -m 'cid'"
					//bat "git push --set-upstream origin develop"
					//bat "git commit -m '[ci skip]'
				}
                
            }
        }
        stage('Publish Artifacts') {
            steps {
                script {
					echo 'Save the assemblies generated from the compilation' 
					def gitCreds = "${env.GITCRED}"
					echo "test ${currentBuild.number}"
					def buildNumber = "test_" + currentBuild.number
					echo "The random number is: ${buildNumber}"
					sshagent (credentials : ["${gitCreds}"]) {
						//sh "git checkout -b develop origin/develop"
						sh "ssh-add /var/jenkins_home/.ssh/id_rsa"
						sh "touch ${buildNumber}.txt"
						sh "git add ."
						sh "git commit -m '[ci-skip] Upversion Build'"
						sh "git push origin develop"
					}
				}
            }
        }
			
    }
	
}
