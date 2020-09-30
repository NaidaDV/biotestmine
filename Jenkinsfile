pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				sshagent(credentials: ['dev-ssh']) {
					sh ''' 
					        ssh -o StrictHostKeyChecking=no -l ubuntu 52.90.174.103 "killall cargoRunLocal"
						ssh -o StrictHostKeyChecking=no -l ubuntu 52.90.174.103 "if ! [ -d /home/ubuntu/biotestmine ]; then mkdir /home/ubuntu/biotestmine; else rm -R /home/ubuntu/biotestmine; mkdir /home/ubuntu/biotestmine; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu 52.90.174.103 "git clone https://github.com/NaidaDV/biotestmine.git /home/ubuntu/biotestmine"
						ssh -o StrictHostKeyChecking=no -l ubuntu 52.90.174.103 ./biotestmine/setup.sh
					'''
				}
			}
		}
	}
}
