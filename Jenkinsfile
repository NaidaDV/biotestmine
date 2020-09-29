pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				sshagent(credentials: ['dev-ssh']) {
					sh ''' 
					        ssh -o StrictHostKeyChecking=no -l ubuntu 18.204.198.82 "if ! [ -d /home/ubuntu/git ]; then mkdir /home/ubuntu/git; else rm -R /home/ubuntu/git; mkdir /home/ubuntu/git; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu 18.204.198.82 "git clone https://github.com/NaidaDV/biotestmine.git /home/ubuntu/git/biotestmine"
						ssh -o StrictHostKeyChecking=no -l ubuntu 18.204.198.82 ./git/biotestmine/setup.sh
					'''
				}
			}
		}
	}
}
