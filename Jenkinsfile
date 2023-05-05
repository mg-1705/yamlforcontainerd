pipeline{
    agent{
        kubernetes {
            
            yamlFile 'containerdwithnerd.yml'
                
        }
    }
    
    environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerlogin')
	}
    stages{
        
        stage('run'){
            steps{
                container('nerdctlcont'){
                    sh 'nerdctl pull busybox'
                    sh 'apt update && apt install git -y'
                    sh 'git clone https://github.com/mg-1705/Dockerizing-a-NodeJS-web-app.git'
                    sh 'nerdctl build -t madhur17/nerdcontla:2 -f Dockerizing-a-NodeJS-web-app/Dockerfile .'
                    sh 'ls -al'
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | nerdctl login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    sh 'nerdctl push madhur17/nerdcontla:2'
                    sh 'sleep 120'
                }
            }
        }
    }
}    
