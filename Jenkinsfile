pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				sshagent(credentials: ['dev-ssh']) {
					sh ''' 
					        ssh -o StrictHostKeyChecking=no -l ubuntu 54.175.78.149 "if [[ -n 'ps | grep java' ]]; then killall java; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu 54.175.78.149 "if ! [ -d /home/ubuntu/biotestmine ]; then mkdir /home/ubuntu/biotestmine; else rm -R /home/ubuntu/biotestmine; mkdir /home/ubuntu/biotestmine; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu 54.175.78.149 "git clone https://github.com/NaidaDV/biotestmine.git /home/ubuntu/biotestmine"
						ssh -o StrictHostKeyChecking=no -l ubuntu 54.175.78.149 ./biotestmine/setup.sh
						ssh -o StrictHostKeyChecking=no -l ubuntu 54.175.78.149 "sleep 420"
						ssh -o StrictHostKeyChecking=no -l ubuntu 54.175.78.149 "killall java"
						ssh -o StrictHostKeyChecking=no -l ubuntu 54.175.78.149 "./biotestmine/gradlew cargoRunLocal > /dev/null 2>&1 &"

					'''
				}
			}
		}
	}
}
