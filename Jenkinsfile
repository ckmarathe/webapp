pipeline{
	agent any 
	environment{
		DOCKER_TAG = getDockerTag() 
	}
	stages{
		stage('Build docker image'){
			steps{
				sh "docker build . -t chetanmarathe/webapp:${DOCKER_TAG}"
			}
		}
		stage('DockerHub Push'){
			steps{
				withCredentials([string(credentialsId: 'dockeruser', variable: 'DOCKERUSER'), string(credentialsId: 'dockerpass', variable: 'DOCKERPASS')]) {
					sh "docker login -u ${DOCKERUSER} -p ${DOCKERPASS}"
			  		sh "docker push chetanmarathe/webapp:${DOCKER_TAG}"    // some block    // some block
				}
			}
		}
	}

}

def getDockerTag(){
	def tag = sh script: "git rev-parse HEAD", returnStdout: true
	return tag
}
