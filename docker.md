# Basic Docker Commands
``` bash
docker images busybox            # Check if the local system has the "busybox" image  
docker search busybox            # Search online registries for the "busybox" image  
docker pull busybox              # Download the "busybox" image  
docker rmi busybox               # Delete the "busybox" image  
docker create -i -t --name foo busybox   # Create a container named "foo" based on the "busybox" image  
docker ps -a                    # View all containers, including stopped ones  
docker ps                        # View running containers  
docker start -i foo              # Start the "foo" container and attach to it interactively  
(Ctrl + P) + (Ctrl + Q)          # Detach from a container without stopping it  
docker attach foo                # Attach to the "foo" container  
docker stop foo                  # Stop the "foo" container  
docker rm foo                    # Delete the "foo" container  
docker run = docker create + docker start   # Create a new container and start it  
```

# Additional Docker Run Options
```bash
docker run --rm --name web httpd  # Create a container named "web" and run the "httpd" image, then remove the container when it exits  
docker run -d httpd               # Create a container and run the "httpd" image in the background  
docker run -d --name web httpd    # Create a container named "web" and run the "httpd" image in the background  
docker rm -f web                  # Forcefully remove a container named "web"  
docker run -d -p 8080:80 httpd    # Create a container, run the "httpd" image in the background, and map container port 80 to host port 8080 (fails if the port is already in use)  
```

# More Docker Run Options
```bash
docker run -d --name web -p 8080:80 httpd  # Create a container named "web," run the "httpd" image in the background, and map container port 80 to host port 8080 (fails if the port is already in use)  
docker exec -it web bash         # Enter the "web" container interactively using the Bash shell  
cat htdocs/index.html            # View the contents of the "index.html" file within the container  
exit                            # Exit the container  
docker exec -it web bash         # Re-enter the "web" container interactively  
echo Hello volume > htdocs/index.html && exit  # Replace the contents of "index.html" with "Hello volume" and exit the container  
curl http://localhost:8080/      # View the contents of "index.html" within the container  
```

# Volume Mounting
```bash
pwd                             # Display the current working directory  
cd ~                            # Change to the home directory  
echo Hello volume > test.html    # Create a "test.html" file  
docker run -d -it -v `pwd`:/usr/local/apache2/htdocs -p 8080:80 httpd  # Run an "httpd" container, bind-mounting the current directory to the container's "/usr/local/apache2/htdocs" directory and mapping container port 80 to host port 8080  
curl http://localhost:8080/test.html  # View the contents of "test.html" within the container (you'll see "Hello volume" since it's bind-mounted)  
```

# Reference 
1. [30 天與鯨魚先生做好朋友 - Docker newbie](https://mileschou.me/ironman/12th/docker-newbie)
