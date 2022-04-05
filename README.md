# Docker-Administration-Commands
This contain the Docker Administration Commands list. The list is not complete and it will be updated by the time of experience. This list is limited but can be improved much more. We always welcome to the community to participate in it. 

### Status of running Docker container

	~$docker version #get the version and info of running/installed docker 
	~$docker images #list number of available images in local repository
	~$docker network ls #list the available networks
 	~$docker ps -a #get list of running and exited container
 	~$docker inspect [container ID]
 	~$docker inspect [Network ID]
  
  #### Note: We can also use the grep command with docker like evaluating the inspect of the container or anything else to get the better result as follow
  
    $ docker inspect mysql | grep -i "entry"
                "Entrypoint": [
                    "docker-entrypoint.sh"
                "Entrypoint": [
                    "docker-entrypoint.sh"
    $ grep -i "CMD\|ENTRYPOINT" Dockerfile-wordpress    
    COPY docker-entrypoint.sh /usr/local/bin/
    ENTRYPOINT ["docker-entrypoint.sh"]
    CMD ["apache2-foreground"]
    $apache2-foreground docker-entrypoint.sh #from the above we can deduce that what command that will be run by the Dockerfile


### Run/Stop/Remove Docker container
 
	~$docker container run [image name] #run the docker container of specified image 
	~$docker container run -d [image name] #run the docker container of specified image in detach mode
	~$docker container stop [you can put container ID first 4character]
 	~$docker container stop $(docker ps -q) #it will stop all the running docker containers
 	~$docker container run -d --name [conatiner name] [image:tag]
	~$docker rm $(docker ps -a) #it will remove/delete all the docker container

### Pull/Push/Remove Docker image

	~$docker images -q #show the images
	~$docker pull [image:tag or without tag] #fetch the image from the DockerHub
	~$docker rmi [image ID] #it will remove the image by ID
	~$docker rmi $(docker images -q) #it will remove all images
	~$docker rmi  -f $(docker images -q) #forcefully remove all the images
	~$docker image prune -a  #This will remove all images without at least one container associated to them.

### For MySQL

	~$docker run -d --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 mysql
	~$docker exec mysql-db mysql -pdb_pass123 -e 'use foo; select * from myTable' #Run the query inside mysql container
 
### Networking

	~$docker container run -d --network none --name alpine-2 alpine #Run the container with no network 
	~$docker run --name alpine-2 --network=none alpine #Both above and this command are seem to same as my knowledge but in Lab this below was successfull 
	~$docker container run -p [host Port]:[container port to expose] -d [image:tag]


### Run Bash command in container

	~$docker container run -d ubuntu sleep 1000
