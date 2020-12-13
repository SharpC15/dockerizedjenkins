node {    
	

    def newApp
    def registry = 'hub.docker.com'
    def registryCredential = 'dockerhub'
	
	stage('Git') {
		git 'https://github.com/SharpC15/dockerizedjenkins.git'
	}
	stage('Build') {
		sh 'npm install'
		/*sh 'npm run bowerInstall'*/
	}
	stage('Test') {
		sh 'npm test'
	}
	stage('Building image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}
	stage('Registring image') {
        docker.withRegistry( "https://registry.hub.docker.com", registryCredential ) {
    		newApp.push 'latest2'
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
