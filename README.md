# docker-thingworx
A dockerfile to dockerize the Thingworx plateform

Tested with TW 7.1.

Thingworx is a platform dedicated to design and run IoT/M2M applications. See http://www.thingworx.com/

**TW is an under licenced software, you need to buy it.**

I have to use it in my work at Rtone (http://rtone.fr) and a Docker container should be useful to share the plateform with colleagues.

Content of the container
------------------------

TW is a java based webapp. It runs on a tomcat-8/jre-8 environnement with some jvm options. TW also needs two directories to store its data.

Installation
------------

 * Add the Thingworx.war file to the build directory. Don't check this into a public github repo, because you probably don't have permissions to redistribute it.
 * `docker build -t thingworx .`
 * `docker run -d --name thingworx -p 8080:8080 thingworx`
 * connect to http://docker:8080/Thingworx
 * default account is Administrator/admin

You can open a shell in the container with: `docker exec -it thingworx bash`

Stop with: `docker stop thingworx`
Start with: `docker start thingworx``

You should use Docker shared volumes to access the TW storage directories (/ThingworxStorage and ThingworxBackupStorage) outside of the container. For example: 

    docker run -d -p 8080:8080 -v $HOME/TW/ThingworxStorage:/ThingworxStorage \
    -v $HOME/TW/ThingworxBackupStorage:/ThingworxBackupStorage thingworx
