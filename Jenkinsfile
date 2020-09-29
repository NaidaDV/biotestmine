pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				sshagent(credentials: ['dev-ssh']) {
					sh '''
						if ! [ -d /home/ubuntu/git ]; then
                				mkdir ~/git
						else
						rm -R ~/git
						mkdir ~/git
                				fi
						ssh -o StrictHostKeyChecking=no -l ubuntu 18.204.198.82 "git clone https://github.com/NaidaDV/biotestmine.git ~/git/biotestmine"
						ssh -o StrictHostKeyChecking=no -l ubuntu 18.204.198.82 ./setup.sh
					'''
				}
			}
		}
	}
}
