pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				sshagent(credentials: ['dev-ssh']) {
					sh ''' 
 					        #ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN "if [ -n $("ps | grep java") ]; then killall java; echo "App not running"; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN "if ! [ -d /home/ubuntu/biotestmine ]; then mkdir /home/ubuntu/biotestmine; else rm -R /home/ubuntu/biotestmine; mkdir /home/ubuntu/biotestmine; fi"
						ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN "git clone https://github.com/NaidaDV/biotestmine.git /home/ubuntu/biotestmine"
						#ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN ./biotestmine/setup.sh
						#ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN "sleep 120"
						#ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN "killall java"
						#ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN "cd ./biotestmine; nohup ./gradlew cargoRunLocal > /dev/null 1>&2 &"
						#ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN "sleep 120"

					'''
				}
			}
		}
		
		/*stage("Test") {
			steps {
				sh '''
				wget -S $DEV_IP_JEN:8080/biotestmine
				curl $DEV_IP_JEN:8080/biotestmine
				'''
			}
		}*/
		
		stage("Test") {
			steps {
				sshagent(credentials: ['dev-ssh']) { 
					sh '''
						ssh -o StrictHostKeyChecking=no -l ubuntu $DEV_IP_JEN cd ./biotestmine; . app_version.sh
					
				        '''
				}
			}
		}
		
	}
}
