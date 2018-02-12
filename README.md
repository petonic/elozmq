# elozmq
Holds dockerfiles for ZMQ for RPI and the i86 HP


## Building the Docker Image
For either architecture (RPI or HP), log onto the machine that
you want to build the Docker Image for, and clone this repo.

```
git clone git@github.com:petonic/elozmq.git
```

CD into the base of the cloned directory and type on of the following (depending upon the architecture):

```
docker build -f docker_rpi/Dockerfile -t rpizmq3 .
```
or
```
docker build -f docker_hp/Dockerfile -t hpzmq3 .
```

The ```hpzmq3``` specifies what you want to tag the Docker Image with.  It can be anything, of course.

## Running the Docker Image

To run the image, cd to the directory that you want to have mapped to ```/z``` in the Docker container.

```
cd test    # This would be the 'test' subdirectory in the repo
```

Then, run the following (substituting to the appropriate architecture (RPI or HP), of course):
```
docker run -it --net=host -v `pwd`:/z hpzmq3
```

You will now be at a BASH prompt in the respective container.  From there you can do the following, for instance:
```
cd /z
./zmq_send # configured for the HP server, using 'eno1' as the network interface
# It will start multicasting phony stock prices
```

On the receiving machines, you can similarly run the image into a Docker container on the RPIs using:
```
cd test    # the 'test' subdir in the repo holding the Python test scripts.
docker run -it --net=host -v `pwd`:/z rpizmq3
# It will start receiving multicasted phony stock prices
```
