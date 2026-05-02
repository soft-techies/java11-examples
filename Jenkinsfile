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
// 		  stage('token') {
//             steps {
//                sh ''' echo "place token here" |docker login -u softechie --password-stdin
// '''
//             }
//         }
// 		 stage('push') {
//             steps { 
//                sh ''' sudo docker push softechie/myjava1:latest
// '''
//             }
//         }
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

    }
}
