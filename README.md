# AWS EC2 + Docker + Nginx Lab

## Goal

The goal of this lab was to create an Ubuntu EC2 instance, connect to it using SSH, install Docker, run an Nginx container, and access the Nginx welcome page through the EC2 public IP address.

## Technologies Used

- AWS EC2
- Ubuntu Server 24.04 LTS
- Docker
- Nginx
- SSH
- Security Groups

## Steps Performed

### 1. Created an EC2 Instance

I created an Ubuntu EC2 instance on AWS.

The instance was configured with:

- Ubuntu Server 24.04 LTS
- t3.micro instance type
- Public IPv4 address enabled
- Key pair for SSH connection

### 2. Configured Security Group

I configured the EC2 Security Group to allow the required traffic:

- SSH traffic on port 22
- HTTP traffic on port 80

SSH was used to connect to the EC2 instance.

HTTP was used to access the Nginx web page from the browser.

### 3. Connected to the EC2 Instance

I connected to the EC2 instance using SSH from my local computer.

Example command:

```bash
ssh -i "key-user5.pem" ubuntu@<EC2_PUBLIC_IP>
```

After connecting successfully, I was inside the Ubuntu server.

### 4. Updated Ubuntu Packages

I updated the package list:

```bash
sudo apt update
```

Then I installed the required packages:

```bash
sudo apt install -y ca-certificates curl
```

### 5. Added Docker Repository

I added Docker's official GPG key and Docker repository to the Ubuntu instance.

Commands used:

```bash
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Then I added the Docker repository:

```bash
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
```

After that, I updated the package list again:

```bash
sudo apt update
```

### 6. Installed Docker

I installed Docker using the following command:

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 7. Verified Docker Installation

I checked the Docker version:

```bash
sudo docker --version
```

I also checked that the Docker service was running:

```bash
sudo systemctl status docker --no-pager
```

Docker was active and running.

### 8. Tested Docker with Hello World

I tested Docker using:

```bash
sudo docker run hello-world
```

The output showed:

```text
Hello from Docker!
```

This confirmed that Docker was installed and working correctly.

### 9. Ran an Nginx Container

I ran an Nginx container using Docker:

```bash
sudo docker run -d --name nginx-lab -p 80:80 nginx:latest
```

This command created and started an Nginx container in the background.

Port 80 on the EC2 instance was mapped to port 80 inside the Nginx container.

### 10. Verified the Nginx Container

I checked that the Nginx container was running:

```bash
sudo docker ps
```

The output showed that the container was running and that port 80 was mapped:

```text
0.0.0.0:80->80/tcp
```

### 11. Tested Nginx Locally

I tested Nginx from inside the EC2 instance:

```bash
curl http://localhost
```

The output returned the default Nginx HTML page.

### 12. Tested Nginx from the Browser

Finally, I opened the EC2 public IP address in the browser:

```text
http://<EC2_PUBLIC_IP>
```

The browser displayed the default Nginx welcome page:

```text
Welcome to nginx!
```

This confirmed that the Nginx container was reachable through the public IP address.

## Screenshots

This repository includes screenshots that show:

- SSH connection to the EC2 instance
- Docker hello-world test
- Nginx container running
- Localhost test with curl
- Nginx welcome page in the browser

Screenshot files included:

- `ssh-connected-to-ec2.png`
- `03-docker-hello-world.png`
- `04-nginx-container-running.png`
- `05-nginx-container-running.png`
- `05-nginx-localhost-test.png`
- `06-nginx-browser-public-ip.png`

## Important Security Note

The private key file used for SSH connection was not uploaded to this repository.

Private key files such as `.pem` files should never be uploaded to GitHub.

## Cleanup

After finishing the lab, the resources should be removed to avoid unnecessary AWS charges.

The Nginx container can be stopped and removed using:

```bash
sudo docker stop nginx-lab
sudo docker rm nginx-lab
```

The EC2 instance should be terminated from the AWS Console when the lab is finished.

## Conclusion

In this lab, I created an Ubuntu EC2 instance, connected to it using SSH, installed Docker, ran an Nginx container, and verified that the Nginx welcome page was accessible through the EC2 public IP address.
