#**Lab 1: Getting to Know Docker on RHEL**

Red Hat Enterprise Linux provides shared services for Docker.  selinux... systemd... What else?


##**1.1 Run an Image and Look Inside**

All actions in this lab will performed by the user *joe*

Are we secure?

    sestatus

Is there any documentation?

    rpm -qd docker-io
    man docker
    man docker-run

What images do we have?

    docker images
    
How do we run an image?

    docker run -i -t rhel7 echo hello
    
Lets look around inside the image.

    docker run -i -t rhel7 bash
    
What's my networking look like in here?

    ip a

    ip r s
    
What's my hostname?

    hostname
    
What processes are running?

    ps aux
    
##**1.2 Saving Content**

Create a file.

    echo "Hello World" >> ~/file1
    
Time to exit.

    exit
    
Did it save my file?

    docker run -i -t rhel7 bash
    
How do I save content?

    echo "Hello World" >> /file2
    
Lets commit.

    exit

    docker ps -l

    docker commit *UUID* file2/container
    ae4b621fc73d0a66bf1e98657dee570043cb7f9910c0b96782a914fee85437f2

    
Now lets see if it saved the file.

    docker images
    docker run -i -t file2/container bash
  
##**1.3 Run an Image and Look Around**

Now that we have explored what's on the inside of a container, let's see what is going on outside of the container.

Let's launch a container and leave it running and confirm it is running.

    docker run -d rhel7
    docker ps

Check out the networking on the host.

    brctl show
    
Check out the bridge

    ip a s docker0
    
What are the firewall rules?

    iptables -nvL -t nat

What is Docker putting on the file system?

    cd /var/lib/docker; ls
    
How do I get the IP address of a running container? Grab the *UUID* of a running container.

    docker ps
    docker inspect *UUID*
    
That's to hard, let's add a filter.

    docker inspect --format '{{ .NetworkSettings.IPAddress }}' *UUID*
    
Put in a docker stop
put in a docker start
show how to create a systemd unit file for a container

    
**Lab 1 Complete!**

<!--BREAK-->

