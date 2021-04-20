### Getting started with Docker 

- Installing Docker in Windows 10
- Running your first container
- Building containers
- Learning what containers are running and removing them

Now, if you are usin Linux or Mac docker-installation will be a pretty straight-forward but in Windows 10 home it can be a pretty daunting task.


I used this sample todo-app built with Nodejs


Create a file named Dockerfile in the same folder as the file package.json with the following contents.

```

FROM node:12-alpine
RUN apk add --no-cache python g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
 
 ```
 
 If you haven’t already done so, open a terminal and go to the app directory with the Dockerfile. Now build the container image using the docker build command.

```
 docker build -t getting-started 
```

Start an app container🔗
Now that we have an image, let’s run the application! To do so, we will use the docker run command (remember that from earlier?).

Start your container using the docker run command and specify the name of the image we just created:

```
 docker run -dp 3000:3000 getting-started
```

Making changes🔗

Lets say you made same new changes in the codebase and now you want to build an updated version of the image.
Follow the same steps as before i.e. 1. Build image and then start container at port 3000 but you'll probably get 
an error

docker: Error response from daemon: driver failed programming external connectivity on endpoint laughing_burnell 
(bb242b2ca4d67eba76e79474fb36bb5125708ebdabd7f45c8eaf16caaabde9dd): Bind for 0.0.0.0:3000 failed: port is already allocated.)

So, what happened? We aren’t able to start the new container because our old container is still running. The reason this is a problem is because that container is using the host’s port 3000 and only one process on the machine (containers included) can listen to a specific port. To fix this, we need to remove the old container.








