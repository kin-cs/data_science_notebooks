## Kubernetes intro

- K8s is a tool for Container Orchestration
  - other similar tools: Docker Swarm & ECS (from AWS)
- it handles mainly [link](https://testdriven.io/blog/running-flask-on-kubernetes/#what-is-container-orchestration):
  - Horizontal scaling
  - Zero-downtime deploys
  - Logging & Monitoring
- Complimentary tools: GoogleContainerTools [link](https://github.com/GoogleContainerTools), e.g.:
  - Skaffold: auto updating the image and contain while you are coding.

### Best practice:
- slim down the image by using the technique **"Multi Stage Builds"**

---
## Deploy ML model in K8s Engine in GCP

- Ref: https://medium.com/analytics-vidhya/deploy-your-first-deep-learning-model-on-kubernetes-with-python-keras-flask-and-docker-575dc07d9e76
- Steps (Docker):
  - 1. create a Compute Engine instance, allow HTTP(S)
  - 2. install docker by
    - i. Login as super user ```$ sudo -s```
    - ii. install docker ```$ sudo apt-get install docker.io```
    - iii. test it ```$ docker```
  - 3. make sure in flask ```app.run(host='0.0.0.0')```
  - 4. create ```Dockerfile``` file, remember to COPY any files you need into this image
    - ```
        FROM python:3.6
        WORKDIR /app
        COPY requirements.txt /app
        ## copy any files you need to this image ##
        RUN pip install -r ./requirements.txt
        COPY main.py /app
        CMD ["python", "main.py"]~
  - 5. build a docker image: ```sudo docker build -t ml-app:latest .```
  - 6. run/create the docker container: ```sudo docker run -d -p 8888:8888 ml-app```
    - check if it's running ```docker ps -a```
  - 7. Done for Docker! Check it with your HTTP request in another machine (tips: remember to use correct POST/GET for your request)
- Step (K8s):
  - 1. (or 2) upload the image to Docker Hub
    - i. create a Docker Hub account
    - ii. login in your docker's instance```sudo docker login```
    - iii. tag your image ```sudo docker tag <your image id> <your docker hub name>/<any app name you like>```
      - check your image id by ```docker image ls``` (not name but id)
    - iv. push the image```sudo docker push <your docker hub name>/<youre created app name>```
  - 2. <NOT WORK YET> (or 1) if you don't push the image to Docker Hub, you need to save the image and send it to K8s instance, and then import it.
    - i. save the docker image as a file ```docker save <image name> > output-name.tar```
    - ii. move the file to Google Storage
      - in GCP, you can do it in your Docker instance with ```gsutil cp 'file-name.tar' 'gs://path-to-your-bucket/file-name.tar'```
    - iii. go to Kubernetes clusters page, connect your cluster, in the cloudshell, download the file with ```gsutil cp 'gs://path-to-your-bucket/file-name.tar' 'file-name.tar' ```
    - iv. then import the image in the cloudshell with connected K8s cluster ```docker load < image-file.tar```
  - 3. now we have image, to run it in K8s, do ```kubectl run ml-app-pod --image=<your-image-name> --port 8888```
    - check if it's running by ```kubectl get pods```, if the STATUS is RUNNING then it's good.
  - 4. expose it to the outside world, ```kubectl expose deployment ml-app-pod --type=LoadBalancer --port 80 --target-port 8888```
    - check if it's working ```kubectl get service```, the EXTERNAL-IP would be shown after a while.
  - 5. DONE!
    - test it with your HTTP request!
  
## Some K8s commands:
- Kill everything: ```kubectl delete daemonsets,replicasets,services,deployments,pods,rc --all```

---
## Docker intro:
- Cloud-Repository, Image and Container
  - Cloud-Repository: ~ github repository, store the image in the 3rd party cloud service
  - Image: all the files and codes in one place
  - Container: able to read or write, based on the image
  - The relationship of above 3 concepts are similar to how Git works

## Some Docker commands:

- list for container: ```docker container ls```, for image ```docker image ls```
- check running container ```docker ps -a```
- stop/remove the container ```docker stop <container name>```
- delete any non-running containers ```docker system prune```
- delete the image ```docker rmi <image name>```

### image: save & load VS container: export & import
- image, we use ```save``` and ```load```
- container, we use ```export``` and ```import```
