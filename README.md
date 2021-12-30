# my-docker-app
A Dockerised React application build into a container and pushed into Docker Hub, i create the index.js file as my landing page an server test page,to check if the server is litening at port:3000 as specified,i ran the command below 
 $ node index.js
 Now inside the dockerfile created
CMD ["node","index.js"]
# Creating the Dockerfile
Created Dockerfile as shown in the repo, this will help in building Docker image for my application 
However i made use of node:current-alpine as my base image beacuse its very light weight to reduce the size of the final docker built image and container image, this serve as part of the optimisation process
Secondly to further optimised my final docker image and container image process i also put some of the files that are not not neccessary to be inside the container image i placed such files in .Dockerignore file
files such as package.json,packge-lockjson.node_modules,.gitignore,Dockerfile
# building the image
I built the image running the neccessary commands
$ docker build -t my-docker-app .
$ docker images
once the docker image was built i then run the container exposed at port:3000
# tested
$ docker run -d -p 3000:3000 good777lord/my-docker-app
$ docker ps
# Creating the deployment object
i created the deployment.yml file for my deployment object for my kubernetes cluster as shown in my repo added all the configurations neccessary as shown , after i ran the command below to apply  the deployment file
 $ kubectl apply -f deployment.yml
 $ kubectl get pods
  $ kubectl get nodes
 $ kubectl get deployments
# Creating the service for the application 
I needed to be able to access the application at port:3000 inside the container so i need to create a service of type:LoadBalancer that will allow the application to be accessble as the targetport:3000 which is the ame as the host port.For internal comnuincation between the pods the service type:clusterip .However in the case i had to create the service.yml file as shown in my repo
$ kubectl apply -f service.yml
 $ kubectl get svc
  $ kubectl describe service my-docker-app-service
 $ kubectl get svc
