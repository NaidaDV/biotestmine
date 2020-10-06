pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				sshagent(credentials: ['key-ssh']) {
					sh '''
						ssh -o StrictHostKeyChecking=no -l ubuntu $PROD_IP_JEN "if [ -n $("ps | grep java") ]; then killall java; echo "App not running"; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu $PROD_IP_JEN "if ! [ -d /home/ubuntu/biotestmine ]; then mkdir /home/ubuntu/biotestmine; else rm -R /home/ubuntu/biotestmine; mkdir /home/ubuntu/biotestmine; rm -R /home/ubuntu/.intermine; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu $PROD_IP_JEN "git clone --branch master https://github.com/NaidaDV/biotestmine.git /home/ubuntu/biotestmine"
						ssh -o StrictHostKeyChecking=no -l ubuntu $PROD_IP_JEN ./biotestmine/setup.sh
						ssh -o StrictHostKeyChecking=no -l ubuntu $PROD_IP_JEN "sleep 120"
						ssh -o StrictHostKeyChecking=no -l ubuntu $PROD_IP_JEN "killall java"
						ssh -o StrictHostKeyChecking=no -l ubuntu $PROD_IP_JEN "cd ./biotestmine; nohup ./gradlew cargoRunLocal > /dev/null 1>&2 &"
						ssh -o StrictHostKeyChecking=no -l ubuntu $PROD_IP_JEN "sleep 120"
					'''
				}
			}
		}
		stage("Test") {
			steps {
				sh '''
				wget -S $PROD_IP_JEN:8080/biotestmine
				'''
			}
		}
	}
	post { 
        	always {
			cleanWs()
		}
	}
}
