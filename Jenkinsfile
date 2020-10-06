pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				sshagent(credentials: ['key-ssh']) {
					sh '''
						ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN_DEV "if [ -n $("ps | grep java") ]; then killall java; echo "App not running"; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN_DEV "if ! [ -d /home/ubuntu/biotestmine ]; then mkdir /home/ubuntu/biotestmine; else rm -R /home/ubuntu/biotestmine; mkdir /home/ubuntu/biotestmine; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN_DEV "git clone https://github.com/NaidaDV/biotestmine.git /home/ubuntu/biotestmine"
						ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN_DEV ./biotestmine/setup.sh
						ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN_DEV "sleep 120"
						ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN_DEV "killall java"
						ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN_DEV "cd ./biotestmine; nohup ./gradlew cargoRunLocal > /dev/null 1>&2 &"
						ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN_DEV "sleep 120"

					'''
				}
			}
		}
		stage("Test") {
			steps {
				sh '''
				wget -S $DEV_IP_JEN_DEV:8080/biotestmine
				curl $DEV_IP_JEN_DEV:8080/biotestmine
				'''
			}
		}	
	}
}
