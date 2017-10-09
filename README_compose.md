### Node-DC/Node-DC-EIS benchmark setup automation

# dependencies
all you need is (love, and):
```
  1. docker
     sudo curl -SsL https://get.docker.com/ | sh -
  2. docker-compose
     sudo curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
  3. sudo chmod +x /usr/local/bin/docker-compose && mkdir -p mongo/data
```
try to reach for the latest.

then try this for Server side:
```
  docker-compose up -d
```

and hope for the magic to start.

# What's next:
you shall see if all went well, two containers, mongodb and nodejs, running and listenning on their ports.
you can do a simple sanity check for nodejs with curl like this:
```
  curl 0.0.0.0:9000
```
if response is "OK", nodejs is alive.

# client side
same same, but different. copy docker-compose-client.yaml file to 
client machine changing the name to compose default format: docker-compose.yaml. then run up command just the same:
```
  docker-compose up -d
```
this container is a bit different beast. it relies on Python and some pip modules
when that container is up, one needs to update its config.js file before starting the load like that:
```
  docker exec -it nodedceis_iclient_1 vi Node-DC-EIS-client/config.js
```
and change the server_ipaddress to the Server ip or FQDN.
restart the container afterwards.

# Running the load
```
  docker exec -ti nodedceis_iclient_1 python runspec.py -f config.json
```

if it doesn't work, don't blame us. blame: https://github.com/Node-DC/Node-DC-EIS/blob/master/README_Docker.md
:)

