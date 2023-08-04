node{
        stage('git checkout'){
            echo "checking out the code from github"
            git 'https://github.com/harshpgoti/insure-me.git'
        }
        
        stage('maven build'){
            sh 'mvn clean package'
        }
        
        stage('build docker image'){
            sh 'docker build -t harshgoti/insure-me:1.0 .'
        }
        
        stage('push docker image to docker hub registry')
        {
            echo 'pushing images to registry'
            
            withCredentials([string(credentialsId: 'docker-hub-password', variable: 'dockerHubPasswd')]) {
                sh "docker login -u harshgoti -p ${dockerHubPasswd}"
                sh 'docker push harshgoti/insure-me:1.0'
            }
        }
        
        stage('configure test-server and deploy insure-me'){
            echo "configuring test-server"
            ansiblePlaybook become: true, credentialsId: 'ssh-key-ansibles', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-test-server.yml'
        }
        
}
