# jenkins-sonar-docker-compose
# This code is a code to deploy a Jenkins and sonarqube server using Docker Compose.

# Definition 

       - SonarQube is an open-source web-based tool for code quality analysis. SonarQube can analyze a wide range of code in different programming languages through plugins.
       - Jenkins is an open source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery.
       - Compose is a tool for defining and running multi-container Docker applications.

#  Prerequisites

    - Create an AWS EC2 instance (Using ubuntu, ) 
    - Conect remotely to this AWS EC2 instance ( you must be in the repository where your aws EC2 key pair is located)
    - Run a command to updating and upgrading linux packages 
        $ Sudo apt-get update | sudo apt-get upgrade -y 

    - Install docker 
        $sudo apt-get install docker.io -y

    - Give ubuntu user permission to run a docker command as administrator 
        $ sudo usermod -aG docker ubuntu

    - log out and log back in for your changes to take efec with the "exit" command and reconnect remotely
        $ exit

2. Install Docker-compose
            
	    Option 1
	- To download and install the Compose CLI plugin, run:
        $ DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
        $ mkdir -p $DOCKER_CONFIG/cli-plugins
        $ curl -SL https://github.com/docker/compose/releases/download/v2.7.0/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose
		
	- Apply executable permissions to the binary:
        $ chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose
	
	- Test the installation.
         $ docker compose version
            you must have "Docker Compose version v2.7.0"
	    
	    option2
    - You can also use this option to install Docker Compose
         $ sudo apt-get install docker-compose 


3. Create and Run a Docker-compose file 

        - create a docker-compose file ( the extension is .yaml)
            $ vim docker-compose.yaml
         
        - Run a docker-compose file 
            $ docker compose up       


4. Configuring servers 

    By now, you are halfway through installing Jenkins successfully. But, before you actually start using it, you need to set it up with basic amenities. How? The first step in setting up Jenkins is to unlock the newly installed Jenkins.

    Assuming you are still logged into the SSH client:

    step 1.    Open your browser and navigate to the IP address of the server followed by port 8080 like jenkins-ip:8080.

    step 2.  After navigating to the link, you will need to unlock Jenkins by providing the administrative password. The administrative password is  stored in /var/lib/jenkins/secrets/initialAdminPassword directory on the server (step two).
         
         -  Unlocking Jenkins Instance

            + Run a command in your running container (jenkins ).
             $ docker exec -it <<jenkins_container_name>> type_of_shell (bash shell, Korn shell,c shell ) 

            +  Run the cat command below to add the administrator password on your machine from the /var/lib/jenkins/secrets/initialAdminPassword directory.
            $ cat /var/lib/jenkins/secrets/initialAdminPassword

            + Copy the password, paste to your jenkins server in your browser and follow the instruction.


    step 3. Configuring a Sonarqube server and creating a tokens 
       Open a new tab in  your browser and navigate to the IP address of the server followed by port 9000 like sonarqube-ip:9000 
    
    - The default configuration are :

        username : admin
        password : admin


    step 4. Install SonarQube Scanner Plugin

    In order for Jenkins to communicate with SonarQube, we need special plugins to make it happen. Simply login to Jenkins and proceed to install tools that will allow us to connect and communicate with SonarQube. Luckily, there is an amazing plugin ready for you to install and configure. Head over to your Jenkins Server Web portal, click on “Manage Jenkins” --> “Manage Plugins” --> Click on the “Available tab” then search for SonarQube. Select “SonarQube Scanner” once it shows up in the list of plugins. Click on “Install without restart” tab then wait for it to complete installing. 

    step 4.  Generate Token in SonarQube Server

    In this step we are going to generate a token that we will use in Jenkins server to connect to it. We already covered the installation of SonarQube Server so head over to your installed instance, log in as Administrator and do the following:Click on your Admin account Icon which will bring up a drop down menu. Click on “My Account“. That will open a new page. On the new page, click on the “Security” tab. A new “Tokens” area will appear. Under “Generate Tokens“, put a name you like then hit “Generate“. 
  A new token will be generated. Copy it since we are going to use it in Jenkins next.


    Step 5: Configure SonarQube in Jenkins
    While still logged into Jenkins as an administrator go to “Manage Jenkins” > “Configure System“. Scroll down to the SonarQube configuration section, click "Add SonarQube", and add the values you will be prompted to provide.
    These include a name you prefer, SonarQube server URL, that is where your SonarQube server is running at then the “Server authentication token“. For the Server authentication token, click on “Add” then “Jenkins” as shown below.
    That will open up the Jenkins Credentials Provider. Leave the domain as it is, and choose “Secret Text” for Kind as shown below. Once that is done, enter the token we created in Step 2 for “Secret“, give it a Name/ID that will match with what the secret is all about, you can add a description if you like then hit “Add“.
    After that is done, scroll through “Server authentication token” and choose the token we have just added. Once that is done, simply hit “Apply” then “Save“.


    Step 6: Create a Project in SonarQube
    Head over to your SonarQube Server, log in as Administrator and create a project by following the following steps. Click on “Administration” > “Projects“. Click on the “Projects” drop down list and click on “Management“. On your far right, close to the top, you will see a tab called “Create Project“.  Click on it and it will bring a form where you will enter the details of your project, that is its name and key. You can key in any value here as you prefer then click on “Create“.
    Your Project will be successfully crated as shown below.
