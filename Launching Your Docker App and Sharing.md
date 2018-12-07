# Launching Your Docker App and Sharing

### Launching Your Docker App
Once you have built your Docker app, you are then ready to run the app!  To run the app call the command

```sh
docker run -p 4000:80 imageName
```
where 4000 is your machine's port, 80 is the Docker container's published port, and imageName is the name of the Docker image you have previously built.

You will see a message that Python is serving your app at http://0.0.0.0:80; however, that message is coming from inside the container, which doesn’t know you mapped port 80 of that container to 4000, making the correct URL http://localhost:4000.

Hit ```CTRL+C``` in your terminal to quit.

>On Windows systems, ```CTRL+C``` does not stop the container. So, first type ```CTRL+C``` to get the prompt back (or open another shell), then type ```docker container ls``` to list the running containers, followed by ```docker container stop <Container NAME or ID>``` to stop the container. Otherwise, you get an error response from the daemon when you try to re-run the container in the next step.


To run the app in the background
```sh
docker run -d -p 4000:80 imageName
```

The long container ID for your app is given. Then you are kicked back to your terminal with you container running in the background. The abbreviated container ID can be seen with ```docker container ls```. Both the long ID and abbreviated ID work interchangeably when running commands.

Use ```docker container stop containerID```to end the process where containerID is the ID of your container.

### Sharing Your Docker App
Docker is completley portable. You can upload the image that you have previously built and run it somewhere else. A Docker registry is a collection of repositories, and a repository is a collection of images. Docker's Command Line Interface (CLI) uses Docker's public registry by default. 
> This example uses Docker's public registry. More options can be viewed on Docker's website via the link at the bottom of this page

##### Log in with your Docker ID
Log into the Docker public registry by running ```docker login```

##### Tagging the image
The notation for associating a local image with a repository on a registry is ```username/repository:tag```. The tag is optional, but recommended, since it is the mechanism that registries use to give Docker images a version. Give the repository and tag meaningful names for the context, such as ```get-started:part2```. This puts the image in the ```get-started``` repository and tag it as ```part2```.

Now, put it all together to tag the image. Run ```docker tag image``` with your username, repository, and tag names so that the image uploads to your desired destination. The syntax of the command is:

```
docker tag image username/repository:tag
```

Run ```docker image ls``` to see your newly tagged image.

##### Publish the image
Upload your tagged image to the repository:

```
docker push username/repository:tag
```
Once complete, the results of this upload are publicly available. If you log in to Docker Hub, you see the new image there, with its pull command.

##### Pull and run the image from the remote repository
From now on, you can use docker run and run your app on any machine with this command:
```
docker run -p 4000:80 username/repository:tag
```
If the image isn’t available locally on the machine, Docker pulls it from the repository.

No matter where ```docker run``` executes, it pulls your image, along with Python and all the dependencies from ```requirements.txt```, and runs your code. It all travels together in a neat little package, and you don’t need to install anything on the host machine for Docker to run it.

That's it for running and sharing your Docker app! Full documentation for running and sharing your Docker app can be found on Docker's [website](https://docs.docker.com/get-started/part2/#run-the-app).