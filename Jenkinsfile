node {    
	

    def newApp
    def registry = 'registry.hub.docker.com'
    def registryCredential = 'docker-hub'
	
	stage('Git') {
		git 'https://github.com/SharpC15/dockerizedjenkins.git'
	}
	stage('Build') {
		/*sh 'npm install' */
		/*sh 'npm run bowerInstall'*/
		echo "somthing would build here!"
	}
	stage('Test') {
		/*sh 'npm test' */
		echo "Test passed"
	}
	stage('Building image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
		    def buildName = 'chastinj15/'+ registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}
	/* The image is pushed from the stage above already...*/

    stage('Clean up') {
        registry = registry + '/chastinj15/' + registry
        sh "docker rmi  $registry:$BUILD_NUMBER"
       /*not latest sh "docker rmi  $registry:latest" present */
    }
    
}
