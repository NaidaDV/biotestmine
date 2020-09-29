pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				sshagent(credentials: ['dev-ssh']) {
					sh '''
						if ! [ -d /home/$USER/git ]; then
                				mkdir /home/$USER/git
						else
						rm -R /home/$USER/git
						mkdir /home/$USER/git
                				fi
						ssh -o StrictHostKeyChecking=no -l ubuntu 192.168.42.12 "git clone https://github.com/NaidaDV/biotestmine.git /home/$USER/git/biotestmine"
						ssh -o StrictHostKeyChecking=no -l ubuntu 192.168.42.12 ./setup.sh
					'''
				}
			}
		}
	}
}
