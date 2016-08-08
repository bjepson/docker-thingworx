# docker-thingworx
A dockerfile to dockerize the Thingworx plateform

Tested with TW 7.1.

Thingworx is a platform dedicated to design and run IoT/M2M applications. See http://www.thingworx.com/

You will need to obtain ThingWorx from PTC. It is available as a 120-day Developer Trial Edition. Sign up for a developer account at http://developer.thingworx.com and visit your dashboard to find the Developer Trial Edition.

The original author had used ThingWorx in his work at Rtone (http://rtone.fr) and a Docker container proved useful to share the platform with colleagues.

Content of the container
------------------------

ThingWorx is a Java based web app. It runs on a tomcat-8/jre-8 environment with some jvm options. ThingWorx also needs two directories to store its data.

Installation
------------

 * Add the Thingworx.war file to the build directory. Don't check this into a public github repo, because you probably don't have permissions to redistribute it.
 * `docker build -t thingworx .`
 * `docker run -d --name thingworx -p 8080:8080 thingworx`
 * connect to http://docker:8080/Thingworx
 * default account is Administrator/admin

You can open a shell in the container with: `docker exec -it thingworx bash`

Stop with: `docker stop thingworx`
Start with: `docker start thingworx`

You should use Docker shared volumes to access the TW storage directories (/ThingworxStorage and ThingworxBackupStorage) outside of the container. For example: 

    docker run -d -p 8080:8080 -v $HOME/TW/ThingworxStorage:/ThingworxStorage \
    -v $HOME/TW/ThingworxBackupStorage:/ThingworxBackupStorage thingworx

If you need to access the Docker container from another computer on the same network, you may need to open port 8080 on your computer's firewall.
