# Setting Up Your Own Git Server and Client

This guide will walk you through setting up your own Git server on Ubuntu and then using it from a Kali Linux instance running on Windows Subsystem for Linux (WSL).

## Part 1: Set Up the Git Server
1. **Update the system packages:**

bash
```
sudo apt update
sudo apt upgrade
```
2. **Install Git:**

bash
```
sudo apt install git
```

3. **Create a git user that will manage the repositories:**

bash
```
sudo adduser git
```
4. **Switch to the git user:**

bash
```
sudo su git
```
or
```
sudo -u <user> -s
```
then
```
cd
```
5. **Create a directory that will hold all the repositories:**

bash
```
mkdir repositories
cd repositories
```
6. ***Create a bare repository for your scripts:**

bash
```
mkdir myscripts.git
cd myscripts.git
git init --bare
```
## Part 2: Set Up the Git Client
1. **On your Kali Linux WSL, first install Git:**

bash
```
sudo apt update
sudo apt install git
```
2. **Configure your Git username and email:**

bash
```
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
3. **Navigate to the directory where your scripts are located and initialize a new Git repository:**

bash
```
cd /path/to/your/scripts
git init
```
5. **Add all your scripts to the repository and make an initial commit:**

bash
```
git add .
git commit -m "Initial commit"
```
6. **Add your Ubuntu server as a remote repository:**

bash
```
git remote add origin git@<Ubuntu-Server-IP>:repositories/myscripts.git
```
7. **Push your scripts to the remote repository:**

bash
```
git push -u origin master
```
Note on SSH Keys
You may need to set up SSH keys to enable password-less communication between your Kali Linux and the Ubuntu server.

8. ***Generate a new SSH key pair on your Kali Linux WSL:**

bash
```
ssh-keygen -t rsa -b 4096 -C "your.email@example.com"
```
9. **Copy the public key to your Ubuntu server:**

bash
```
ssh-copy-id git@<Ubuntu-Server-IP>
```
Cloning the Repository on the Client Side
Navigate to the directory where you want the scripts to be cloned.

bash
```
cd ~
mkdir scripts
cd scripts
```
## Part 3: Clone Repo to client
1. **Clone the repository from your Ubuntu server:**

bash
```
git clone git@<Ubuntu-Server-IP>:repositories/myscripts.git
```
2. **Pull the latest changes (if any):**

bash
```
cd myscripts
git pull
```
Remember to replace **'Your Name'**, **'your.email@example.com'**, and **'<Ubuntu-Server-IP>'** with your actual name, email, and the IP address of your Ubuntu server, respectively.
