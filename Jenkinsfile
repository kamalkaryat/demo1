def remote = [:]
remote.name = 'test'
remote.host = '65.0.95.248'			//EC2-PublicIP
remote.port = 22
remote.allowAnyHosts = true
pipeline {
    agent any
     stages {
        stage('Git Clone') {
            steps {
                // Get some code from a GitHub repository. 
		// githubcreds: arbitary_name given while adding github credentials in jenkins
                git branch: 'main', credentialsId: 'githubcreds', url: 'https://github.com/kamalkaryat/demo1'
            }
        }
     stage('Deployment'){
        steps {
            script {
             // move the new changed 
	     //	ubuntucred: arbitary_name given while adding vm/cloud-vm credentials in jenkins
             withCredentials([usernamePassword(credentialsId: 'ubuntucred', passwordVariable: 'pass', usernameVariable: 'user')]) {
             remote.user = user
             remote.password = pass
             sshPut remote: remote, from: "index.html", into: "/var/www/html"
             }
           }
          }
        }
      }
}
