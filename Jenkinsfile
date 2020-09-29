pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				sshagent(credentials: ['dev-ssh']) {
					sh ''' 
					        ssh -o StrictHostKeyChecking=no -l ubuntu 3.83.135.79 "ps -ef | grep java | awk '{print $2}' | xargs kill"
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.83.135.79 "if ! [ -d /home/ubuntu/biotestmine ]; then mkdir /home/ubuntu/biotestmine; else rm -R /home/ubuntu/biotestmine; mkdir /home/ubuntu/biotestmine; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.83.135.79 "git clone https://github.com/NaidaDV/biotestmine.git /home/ubuntu/biotestmine"
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.83.135.79 ./biotestmine/setup.sh
					'''
				}
			}
		}
	}
}
