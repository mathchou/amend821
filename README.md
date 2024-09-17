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
  - deploy docker and docassemble on that instance
  - buy domain name (can be through amazon Route 53, also can be done directly through amazon Lightsail)
  - point domain name to static IP address (A type record)
  - allow time for DNS to propogate
  - visit domain name to access docassemble web interface
  - create/package/install interview on the system
  - change default interview to point to correct one
  - set up email sending (didn't get to this)
  - set up data management (didn't get to this)

## Deploying docker on instance

[Guide](https://docassemble.org/deploy.html)

## Encrypting Nginx Website

[Guide for Amazon Lightsail](https://docs.aws.amazon.com/lightsail/latest/userguide/amazon-lightsail-using-lets-encrypt-certificates-with-nginx.html)

