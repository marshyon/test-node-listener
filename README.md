# Simple Node Listener App

This simple Node application is meant to be used for testing Docker based infrastructure such as Kubernetes, Swarm, OpenShift etc. 

It is configured to receive HTTP POST requests at `/data` and logs the JSON that is posted to stdout.

If configured, the environment variable `SYSTEM_COMMAND` is read and run and its output logged to stdout.

# Stand alone

install dependencies :

```
npm install
```

running with no command configured :

```
node app.js
```

running with a command configured in Powershell :

```
$Env:SYSTEM_COMMAND="pwd"; node .\app.js
```

or in Bash :

```
SYSTEM_COMMAND="pwd"; node .\app.js
```

# Docker 

build & run locally :

```
docker build -t test-node-listener:latest .
docker run --name test-node-listener -p 4000:4000 -e SYSTEM_COMMAND="ls -al" -d --rm test-node-listener
docker logs -f test-node-listener
# <cntrl-c> when you get fed up of tailing log output
...
# to stop and remove (because --rm was used to auto remove) running container ...
docker stop test-node-listener 
```

push to docker and run from uploaded image :

```
docker tag test-node-listener marshyon/test-node-listener
docker push marshyon/test-node-listener
docker run -p 9090:8080 -d --name test-node --rm marshyon/test-node-listener
...
# to stop and remove (because --rm was used to auto remove) running container ...
docker stop test-node-listener 
```

___replacing marshyon with your docker hub account name___

