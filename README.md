# Create docassemble docker server on Amazon Lightsail Instance

Generally, follow this setup guide: [Guide](https://projects.suffolklitlab.org/legal-tech-class/docs/practical-guide-docassemble/setup-server/)

I skipped over the S3 storage stuff.

If there are issues with starting the container
`docker run --env-file=C:/Users/mokec/PycharmProjects/Ammendment_821/env.list -v dabackup:/usr/share/docassemble/backup -d -p 80:80 -p 443:443 --name amend821host --restart always --stop-timeout 600 jhpyle/docassemble`
such as "daemon requires blah blah blah" try stopping and restarting docker:

`docker info
sudo systemctl stop docker
sudo systemctl stop docker.socket
sudo systemctl start docker.socket
sudo systemctl start docker`

## Outline
  - buy amazon lightsail instance of correct power (RAM/CPU)
  - attach static IP address
  - deploy docker on that instance
  - buy domain name (can be through amazon Route 53, also can be done directly through amazon Lightsail)
  - point domain name to static IP address (A type record)
  - allow time for DNS to propogate
  - visit domain name to access docker web interface
  - create/package/install interview on the system
  - change default interview to point to correct one
  - set up email sending (didn't get to this)
  - set up data management (didn't get to this)

## Deploying docker on instance

[Guide](https://docassemble.org/deploy.html)

## Encrypting Nginx Website

[Guide for Amazon Lightsail](https://docs.aws.amazon.com/lightsail/latest/userguide/amazon-lightsail-using-lets-encrypt-certificates-with-nginx.html)




# 






# Create docassemble docker server on home computer

We will start from scratch in this section. Note that we are simply summarizing relevant info from [https://docassemble.org/docs/docker.html](https://docassemble.org/docs/docker.html). See that link for more complete information.

## Computer configuration help

  - In order to stop docker from taking all the RAM, see here: [Useful links:
Freeing up RAM from vmmem](https://stackoverflow.com/questions/64165192/stopping-vmmem-from-using-ram).

## Starting the container and server

  1. We want to start a container with a persistent volume to export data. See [https://docassemble.org/docs/docker.html#persistent](https://docassemble.org/docs/docker.html#persistent)
     - Code to run: `docker run --env-file=C:/Users/mokec/PycharmProjects/Ammendment_821/env.list -v dabackup:/usr/share/docassemble/backup -d -p 80:80 -p 443:443 --name amend821host --restart always --stop-timeout 600 jhpyle/docassemble`

# (re)-Starting server on home computer 

This section assumes that the docker container has already been initialized with a persistent volume and correct port mappings.

  1. Open powershell as admin
     - `docker container start <mycontainer>`
     - (getting into docker shell: `docker exec -it <mycontainer> bash`)
  2. Wait 5 minutes for container to start up. Access via [https://localhost](https://localhost) or [https://karchou.dynamic-dns.net](https://karchou.dynamic-dns.net) which is where it's set up currently
     - if it isn't started, get into docker shell via: `docker exec -it <mycontainer> bash`
     - to list running services in the container: `supervisorctl status`
     - can reset everything by `supervisorctl start reset`
     - see [https://docassemble.org/docs/docker.html#troubleshooting](https://docassemble.org/docs/docker.html#troubleshooting)
