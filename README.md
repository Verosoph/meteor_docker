# meteor_docker
how to create a docker container with meteor and angular.js

## Step 1
Configure the docker-compose.yml

```
app:
  image: username/containername
  ports:
    - "8080:3000"
  links:
    - mongo
  environment:
    - ROOT_URL=http://127.0.0.1
 
    - MONGO_URL=mongodb://mongo:27017/meteor
 
mongo:
  image: mongo:latest
  command: mongod --storageEngine=wiredTiger
```

## Step 2
Build the docker container

```
docker build -t username/containername .
```
You may need sudo
And . if you are at the same folder

## Step 3
Start the docker container
```
docker-compose up -d
```
You may need sudo
And you need at the same folder as your docker-compose.yml

Autostart your docker on server start
Go to /etc/systemd/system
Create a .service file → e.g. appname.service

```
[Unit]
Description=TheServiceName
Requires=docker.service
After=docker.service
 
[Service]
WorkingDirectory=/folder/of/your/docker
Type=oneshot
RemainAfterExit=yes
User=root
 
ExecStart=/usr/bin/docker-compose up -d
 
[Install]
WantedBy=multi-user.target
```
Enable your service
```
systemctl enable appname.service
```



