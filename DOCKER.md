#Prerequisites
- nodejs
- npm
- docker
- nodemon (npm install -g nodemon)

#Preparing your environment

Please follow the following steps to set up a local sandbox environment for development.

##Installing Hyperledger locally
Hyperledger runs locally in two docker containers: membersrvc for the Certificate Authority and peer for our local node. Remember to replace `path/to/project` with the actual path to your project. 

To prepare them do (from the project directory):

> docker build --tag membersrvc docker/membersrv

> docker build --tag peer docker/peer

> docker run -d --name membersrvc membersrvc

> docker run -d --privileged --name peer -p 5000:5000 -v /path/to/project/chaincode:/opt/go/src/chaincode --link membersrvc peer

If you want to see the logs you can also run the container without the -d flag or do `docker logs --tail 20 -f peer`. See the docker documentation for more info.

The first time you run the peer it has to get the base image for the chaincode containers. This will take a while.

Sidenote: there is some docker inception going on here: chaincode is executed in docker containers. Ideally we would get the base image during the build phase but running docker inside docker requires the --privileged flag, which is not available during build.

##Running hyperledger locally
> docker start membersrvc

> docker start peer

Check if it's running by visiting `localhost:5000/chain` in your browser.:
