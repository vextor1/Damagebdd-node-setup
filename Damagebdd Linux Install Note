Beginner Documentation: Linux, Docker, DamageBDD Stack, and Tor Onion Service Setup

Table of Contents

1. Introduction
2. Prerequisites
3. Linux Installation Notes
4. System Update
5. Docker Installation
6. Docker Compose Installation
7. Docker Verification
8. Understanding Docker Basics
9. DamageBDD Stack Setup
10. Common Docker Commands
11. Managing the DamageBDD Stack
12. Tor Installation
13. Get the Onion Address
14. Verify the Onion Service
15. Troubleshooting
16. Finding the node/account address
17. First synchronization proof
18. Best Practices
19. Useful Commands

1. Introduction

This guide walks through setting up a complete development environment consisting of:

* Ubuntu Linux
* Docker
* Docker Compose
* DamageBDD application stack
* Tor Onion Service

After completing this guide, you should be able to:

* Install Linux
* Install Docker
* Run Docker containers
* Start and stop the DamageBDD stack
* Expose your application through a `.onion` address

2. Prerequisites

Recommended specifications:

| Component | Minimum                      |
| --------- | ---------------------------- |
| RAM       | 4 GB                         |
| CPU       | Dual Core                    |
| Storage   | 30 GB Free                   |
| Internet  | Required                     |
| OS        | Ubuntu 22.04 or Ubuntu 24.04 |

3. Linux Installation Notes

Step 1: Download Ubuntu

Download Ubuntu Desktop from the official website.

Recommended version:

* Ubuntu 22.04 LTS
* Ubuntu 24.04 LTS

Step 2: Create Bootable USB

Use one of the following tools:

* Rufus (Windows)
* Balena Etcher
* Ventoy

Flash the Ubuntu ISO to a USB drive.

Step 3: Boot from USB

Restart your computer.

Open the Boot Menu (usually F12, ESC, or F9).

Choose the USB device.

Step 4: Install Ubuntu

Select:

Install Ubuntu

Recommended settings:

* English language
* Normal installation
* Install third-party software
* Automatic partitioning (for beginners)

Create:

* Username
* Password

Complete installation.

Restart the computer.

Remove the USB drive.

4. Update the System

Always update the system before installing software.

```bash
sudo apt update
sudo apt upgrade -y
```

(Optional)

```bash

```sudo apt autoremove -y```

5. Docker Installation

⚠️ Important: Do Not Delete Docker Volumes or Secrets

DamageBDD stores persistent data such as blockchain state, databases, cryptographic keys, and other application data in Docker volumes and managed secrets.

Avoid running commands that remove persistent storage unless you intentionally want to reset the node.

In particular, use caution with:

docker compose down -v
docker volume rm ...
docker system prune --volumes

Deleting volumes or secrets may permanently remove:

blockchain synchronization data
node identity
account or wallet information
configuration secrets
application databases

If you need to clean up Docker resources, prefer:

docker compose down

which stops and removes containers without deleting persistent data.

Stop the conflicting process or change the application's listening port.


Remove old Docker versions

```bash
sudo apt remove docker docker-engine docker.io containerd runc
```

Install dependencies

```bash
sudo apt install \
ca-certificates \
curl \
gnupg \
lsb-release -y
```
Add Docker GPG Key

```bash
sudo mkdir -p /etc/apt/keyrings
```

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

Add Docker Repository

```bash
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list
```

Install Docker

```bash
sudo apt update
```

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

Enable Docker

```bash
sudo systemctl enable docker
```

```bash
sudo systemctl start docker
```

Allow Current User

```bash
sudo usermod -aG docker $USER
```

Log out and log back in.

6. Docker Compose

Modern Docker includes Docker Compose as a plugin.

Check version:

```bash
docker compose version
```

Example output:

```
Docker Compose version v2.x.x
```
7. Verify Docker

Run:

```bash
docker --version
```

Run:

```bash
docker compose version
```

Test Docker:

```bash
docker run hello-world
```

Expected message:

```
Hello from Docker!
```

8. Docker Basics

Images

Images are templates used to create containers.

List images:

```bash
docker images
```
Containers

Running instances of images.

List running containers:

```bash
docker ps
```

List all containers:

```bash
docker ps -a
```
Networks

```bash
docker network ls
```
Volumes

```bash
docker volume ls
```
9. DamageBDD Stack Setup

Note: Replace `damagebdd` below with the actual project directory if it has a different name.

Clone the repository:

```bash
git clone https://github.com/DamageBDD/DamageBDD.git
```

Enter the project:

```bash
cd DamageBDD
```

Verify files:

```
docker-compose.yml
Dockerfile
.env
README.md
```
Build the stack

```bash
docker compose up --build -d
```

Start the stack

```bash
docker compose up
```

Run in background:

```bash
docker compose up -d
```
Stop the stack

```bash
docker compose down
```

Restart

```bash
docker compose restart
```

Rebuild

```bash
docker compose up --build
```

10. DamageBDD Stack Commands

Start

```bash
docker compose up -d
```

Stop

```bash
docker compose down
```

Restart

```bash
docker compose restart
```

Build

```bash
docker compose build
```

View Logs

```bash
docker compose logs
```

Live logs:

```bash
docker compose logs -f
```

List Services

```bash
docker compose ps
```

Execute Shell

```bash
docker compose exec <service-name> bash
```

Example:

```bash
docker compose exec backend bash
```

Recreate Containers

```bash
docker compose up --force-recreate
```

Remove Unused Resources

```bash
docker system prune
```

Remove everything unused:

```bash
docker system prune -a
```

11. Managing the Stack

Check Container Status

```bash
docker ps
```

Check Logs

```bash
docker logs <container-name>
```

Restart One Container

```bash
docker restart <container-name>
```

Stop One Container

```bash
docker stop <container-name>
```

Remove Container

```bash
docker rm <container-name>
```

First health check

Immediately after the containers start, verify that the web service is responding.

Open:

http://localhost:4888/version/

A successful response confirms that:

Docker containers are running
DamageBDD Web API is available
Port 4888 is correctly exposed

If this endpoint does not respond, check:

docker compose ps
docker compose logs -f

12. Tor Onion Setup Notes

Install Tor

```bash
sudo apt install tor -y
```

Enable Tor:

```bash
sudo systemctl enable tor
```

Start Tor:

```bash
sudo systemctl start tor
```

Verify:

```bash
sudo systemctl status tor
```

Configure Onion Service

Edit:

```bash
sudo nano /etc/tor/torrc
```

Add:

```text
HiddenServiceDir /var/lib/tor/damagebdd/

HiddenServicePort 80 127.0.0.1:4888
```

Meaning:

* Onion Service listens on port 80.
* Traffic forwards to localhost port 4888.

Restart Tor:

```bash
sudo systemctl restart tor
```

13. Get the Onion Address

View:

```bash
sudo cat /var/lib/tor/damagebdd/hostname
```

Example:

```
abcdefghijklmnopqrstuvwxyz1234567890.onion
```

This is your public Onion address.

14. Verify the Onion Service

Check Tor:

```bash
sudo systemctl status tor
```

Check if your application is running:

```bash
docker ps
```

Ensure the application listens on:

```
127.0.0.1:4888
```

Open the `.onion` address using the Tor Browser.

If configured correctly, your application should load.

15. Troubleshooting

Docker Permission Denied

```bash
sudo usermod -aG docker $USER
```

Log out and back in.

---

Docker Service Not Running

```bash
sudo systemctl restart docker
```

Tor Service Fails

Inspect logs:

```bash
journalctl -u tor
```

Check configuration:

```bash
sudo nano /etc/tor/torrc
```

Container Keeps Restarting

Inspect logs:

```bash
docker compose logs
```

or

```bash
docker logs <container-name>
```

Port Already in Use

Find the process:

```bash
sudo lsof -i :4888
```

16. Finding the node/account address

Once the stack has started and the node has initialized, locate the generated account or node address from the logs.
or top right corner of your node dashboard (WALLET)

View live logs:

docker compose logs -f

Look for output similar to:

Account Address:
ak_2be8qTvAR7K8M13MU8REw...

or

Node Address:
ak_2be8qTvAR7K8M13MU8REw...

Copy this address, as it is typically required for:

node registration
peer identification
network participation
configuration of other nodes

If the logs are extensive, search for the keywords:

address
Account
Node
wallet

17. First synchronization proof

After startup, confirm that synchronization has begun.

Run:

docker compose logs -f

Evidence of a successful first sync generally includes messages indicating that the node is:

connecting to peers
downloading blockchain data
processing blocks
increasing synchronization height

For example:

Connected to peer ...
Synchronizing...
Imported block ...

or

Current block height:

Seeing these messages confirms that the node is actively joining the network.

18. Best Practices

* Keep Ubuntu updated regularly.
* Use Docker Compose to manage multi-container applications.
* Store secrets in environment variables or a `.env` file rather than hardcoding them.
* Back up Docker volumes that contain important data.
* Monitor container logs for errors and performance issues.
* Keep Tor, Docker, and the operating system updated with security patches.
* Use version control (such as Git) for project configuration files.

19. Useful Commands

| Task                    | Command                                            |
| ----------------------- | -------------------------------------------------- |
| Update system           | `sudo apt update && sudo apt upgrade -y`           |
| Docker version          | `docker --version`                                 |
| Compose version         | `docker compose version`                           |
| List images             | `docker images`                                    |
| List running containers | `docker ps`                                        |
| List all containers     | `docker ps -a`                                     |
| Start stack             | `docker compose up -d`                             |
| Stop stack              | `docker compose down`                              |
| Restart stack           | `docker compose restart`                           |
| Rebuild stack           | `docker compose up --build`                        |
| View logs               | `docker compose logs -f`                           |
| Execute shell           | `docker compose exec <service> bash`               |
| List networks           | `docker network ls`                                |
| List volumes            | `docker volume ls`                                 |
| Install Tor             | `sudo apt install tor -y`                          |
| Restart Tor             | `sudo systemctl restart tor`                       |
| Tor status              | `sudo systemctl status tor`                        |
| View Onion hostname     | `sudo cat /var/lib/tor/my_hidden_service/hostname` |
