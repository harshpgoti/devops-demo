
node{
    stage('code checkout'){
        echo 'checking repo code cloned'
        git 'https://github.com/harshpgoti/insure-me.git'
    }
    
    stage('code build'){
        echo 'building app, compile, test and create pkg'
        sh 'mvn clean package'
    }
    
    stage('build docker image'){
        sh 'docker build -t harshgoti/insure-me:1.0 .'
    }
        
    stage('push docker image to docker hub registry')
    {
        echo 'pushing images to docker hub registry'
        withCredentials([string(credentialsId: 'dockerHubPasswd', variable: 'dockerHubPasswd')]) {
            sh "docker login -u harshgoti -p ${dockerHubPasswd}"
            sh 'docker push harshgoti/insure-me:1.0'
        }
    }
}