# jenkins-sonar-docker-compose
This code is a code to deploy a Jenkins and sonarqube server using a dockerfile.

Defiinition 

       - SonarQube is an open-source web-based tool for code quality analysis. SonarQube can analyze a wide range of code in different programming languages through plugins.
       - Jenkins is an open source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery.
       - Compose is a tool for defining and running multi-container Docker applications.

1.Pre-requite 

    - Create an AWS EC2 instance (Using ubuntu, ) 
    - Conect remotely to this AWS EC2 instance ( you must be in the repository where your aws EC2 key pair is located)
    - Run a command to updating and upgrading linux packages 
        $ Sudo apt-get update | sudo apt-get upgrade -y 

    - Install docker 
        $sudo apt-get install docker.io -y

    - Give ubuntu user permission to run a docker command as administrator 
        $ sudo usermod -aG docker ubuntu

    - shut down the machine with "EXIT" command and reconnect remotely

2. Install Docker-compose
	- To download and install the Compose CLI plugin, run:
        $ DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
        $ mkdir -p $DOCKER_CONFIG/cli-plugins
        $ curl -SL https://github.com/docker/compose/releases/download/v2.7.0/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose
		
	- Apply executable permissions to the binary:
        $ chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose
	
	- Test the installation.
         $ docker compose version
            you must have "Docker Compose version v2.7.0"
    - You can also run a command to install 
         $ sudo apt-get install docker-compose 

3. Create and Run a Docker-compose file 

        - create a docker-compose file ( the extension is .yaml)
            $ vim docker-compose.yaml
         
        - Run a docker-compose file 
            $ docker compose up       

        
