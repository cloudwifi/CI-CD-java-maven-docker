node {
    // reference to maven
    // ** NOTE: This 'maven-3.5.2' Maven tool must be configured in the Jenkins Global Configuration.   
    def mvnHome = tool 'maven-3.5.2'

    // holds reference to docker image
    def dockerImage
    // ip address of the docker private repository(nexus)
 
    def dockerImageTag = "devopsexample${env.BUILD_NUMBER}"
    
    stage('Clone Repo') { // for display purposes
      // Get some code from a GitHub repository
         git 'https://github.com/cloudwifi/CI-CD-java-maven-docker.git'
      // Get the Maven tool.
      // ** NOTE: This 'maven-3.5.2' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'maven-3.5.2'
    }    
  
    stage('Build Project') {
      // build project via maven
      sh "'${mvnHome}/bin/mvn' clean install"
    }
		
    stage('Build Docker Image') {
      // build docker image
      dockerImage = docker.build("devopsexample:${env.BUILD_NUMBER}")
    }
   	  
    stage('Deploy Docker Image and login'){
      
      echo "Docker Image Tag Name: ${dockerImageTag}"
	  
        sh "docker images"
        sh "docker login -u naveenjangid22 -p kota@1234# "// put PWD
	
}
    stage('Docker push'){
       // docker images | awk '{print $3}' | awk 'NR==2'
	// sh "docker images | awk '{print $3}' | awk 'NR==2'"
	//sh echo "Enter the docker lattest imageID"
	//sh "read imageid"
	   sh "docker tag c269404e091c   naveenjangid22/myapplication" //must change the name and tag no
       sh "docker push   naveenjangid22/myapplication"
  }
}
