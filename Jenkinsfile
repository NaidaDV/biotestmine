pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				sshagent(credentials: ['dev-ssh']) {
					sh ''' 
 					        #ssh -o StrictHostKeyChecking=no -l ubuntu 3.83.87.128 [ -n  $("ps | grep java") ] && killall java || echo "App not running"
					        ssh -o StrictHostKeyChecking=no -l ubuntu 3.92.239.186 "if [ -n $("ps | grep java") ]; then killall java; echo "App not running"; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.92.239.186 "if ! [ -d /home/ubuntu/biotestmine ]; then mkdir /home/ubuntu/biotestmine; else rm -R /home/ubuntu/biotestmine; mkdir /home/ubuntu/biotestmine; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.92.239.186 "git clone https://github.com/NaidaDV/biotestmine.git /home/ubuntu/biotestmine"
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.92.239.186 ./biotestmine/setup.sh
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.92.239.186 "sleep 120"
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.92.239.186 "killall java"
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.92.239.186 "cd ./biotestmine; nohup ./gradlew cargoRunLocal > /dev/null 1>&2 &"
						ssh -o StrictHostKeyChecking=no -l ubuntu 3.92.239.186 "sleep 120"

					'''
				}
			}
		}
	}
}
