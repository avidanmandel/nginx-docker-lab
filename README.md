# AWS EC2 + Docker + Nginx Lab

## Goal

The goal of this lab was to create an Ubuntu EC2 instance, connect to it using SSH, install Docker, run an Nginx container, and access the Nginx welcome page through the public IP address.

## Steps Performed

1. Created an Ubuntu EC2 instance.
2. Configured Security Group rules:
   - SSH on port 22
   - HTTP on port 80
3. Connected to the EC2 instance using SSH.
4. Installed Docker on Ubuntu.
5. Verified Docker installation using hello-world.
6. Ran an Nginx container using Docker.
7. Verified that the Nginx container was running with docker ps.
8. Tested Nginx locally using curl.
9. Opened the EC2 public IP address in the browser and saw the Nginx welcome page.

## Commands Used

```bash
sudo apt update
sudo apt install -y ca-certificates curl

sudo docker --version
sudo systemctl status docker --no-pager
sudo docker run hello-world

sudo docker run -d --name nginx-lab -p 80:80 nginx:latest
sudo docker ps
curl http://localhost


Screenshots
This repository includes screenshots for:

SSH connection to the EC2 instance
Docker hello-world test
Nginx container running
Localhost curl test
Nginx welcome page in the browser
