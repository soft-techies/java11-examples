pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
               git 'https://github.com/openwriteup/java11-jenkins.git'
            }
        }
	  stage('build') {
            steps {
               sh '''sudo docker build -t softechie/myjava1:latest -f dockerfile .
'''
            }
        }
		  stage('token') {
            steps {
               withCredentials([usernamePassword(credentialsId: 'dockerhubId', passwordVariable: 'myPass', usernameVariable: 'userName')])
				{
				
        sh '''echo $myPass |sudo docker login -u $userName --password-stdin
		sudo docker push softechie/myjava1:latest
'''
            }
        }}
		 stage('trivy') {
            steps { 
               sh ''' sudo apt-get install wget gnupg
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
'''
            }
        }
		stage('trivyScan') {
            steps {
               sh '''trivy image --format json --output result.json  --severity HIGH,CRITICAL softechie/myjava1:latest '''
				archiveArtifacts artifacts: 'result.json', followSymlinks: false
            }
        }
		 stage('mailing') {
            steps {
	mail bcc: '', body: 'echo jobstatus ', cc: '', from: 'aradhanaprabhakar98@gmail.com', replyTo: '', subject: 'Pipeline status', to: 'aradhanaprabhakar98@gmail.com'
    slackSend channel: 'jenkinswp', message: 'hi to slack', teamDomain: 'jenkins-m0p2806', tokenCredentialId: 'nqWNtX0igbDF04aFPMXqmUrR'    
			}
 }

    }
}
