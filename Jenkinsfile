pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				sshagent(credentials: ['dev-ssh']) {
					sh ''' 
					        ssh -o StrictHostKeyChecking=no -l ubuntu 3.82.212.2 "killall cargoRunLocal"
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.82.212.2 "if ! [ -d /home/ubuntu/biotestmine ]; then mkdir /home/ubuntu/biotestmine; else rm -R /home/ubuntu/biotestmine; mkdir /home/ubuntu/biotestmine; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.82.212.2 "git clone https://github.com/NaidaDV/biotestmine.git /home/ubuntu/biotestmine"
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.82.212.2 ./biotestmine/setup.sh
					'''
				}
			}
		}
	}
}
