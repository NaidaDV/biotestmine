pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				sshagent(credentials: ['dev-ssh']) {
					sh ''' 
					        ssh -o StrictHostKeyChecking=no -l ubuntu 18.204.198.82 "if ! [ -d /home/$USER/git ]; then mkdir /home/$USER/git; else rm -R /home/$USER/git; mkdir /home/$USER/git; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu 18.204.198.82 "git clone https://github.com/NaidaDV/biotestmine.git /home/$USER/git/biotestmine"
						ssh -o StrictHostKeyChecking=no -l ubuntu 18.204.198.82 ./setup.sh
					'''
				}
			}
		}
	}
}
