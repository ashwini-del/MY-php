## Install LAMP Stack on Debian / Redhat with Ansible
while installing php 5.4 not need to mention yum intall php54 once do yum install php it by default takc php 5.4
/etc/yum.repo.d/
vim /etc/ssh/sshd_config
vim .ssh/authorized_keys
systemctl restart sshd
php - 5.6
sudo ansible -m ping -i hosts web
sudo ansible-playbook -i hosts main.yml 
sudo ansible-playbook -i hosts main.yml --extra-vars "install_firewall=no"

 yum repo path in linux ==/etc/yum.repo.d

we cant set environment variable path in .bashrc file - using export path for all application
php specific version

For RHEL 7 and CentOS 7, the default PHP version is 5.4. For RHEL 8 and CentOS 8, the default PHP version is 7.2. For Fedora, the default PHP version varies based on the specific release, but it's usually one of the latest PHP versions.
do we need to install firewall on ubuntu 
for apache2
It depends on your use case and security requirements. Installing a firewall is a good security practice to restrict incoming and outgoing traffic on a server. In the case of an Apache2 server, it is recommended to install a firewall to block unauthorized access to the server and prevent potential security threats.

The most commonly used firewall in Ubuntu is ufw (Uncomplicated Firewall). It is a user-friendly firewall configuration tool that can be easily managed through the command line. You can install it by running the following command:

csharp
Copy code
sudo apt-get install ufw

In this Task I am going to setup multiple client servers quickly with LAMP . The client servers are like  Debian and Redhat . For setting up LAMP I have used ansible roles. Playbook is made as such it is easily customizable and deployable on mutiple clients(Debian and Redhat) with task specific to each client will be executed using import_tasks module and when condition. 

do we need to install firewall on linux 
for apache2

Yes, it is highly recommended to install a firewall on Linux servers that run Apache2. This provides an extra layer of security and helps prevent unauthorized access to the server. A firewall can help block malicious traffic, control incoming and outgoing traffic, and allow only the necessary services and protocols to be accessible.

There are several firewall options available for Linux, including iptables, ufw, and firewalld. These firewalls can be easily installed and configured to protect your Apache2 server.


is apache2 is need for php page running
Yes, Apache2 is required to run PHP pages. Apache is a web server that can serve HTML, PHP, and other web content, while PHP is a server-side scripting language used to dynamically generate content on web pages. The Apache2 module mod_php is needed to process PHP code in an Apache environment.
## Pre-requisites

- Used Ansible Master server as Ubuntu and Client servers on Amazon Linux
- Ansible Master server is installed with Ansible2.
## Resources Used
- Amazon Linux 2 
- Ubuntu
- Mysql
- PHP
- Ansible2
## Included roles
- Devops Internal Ansible - Setup lamp on all  client systems.

## Actions Performed
- Installs Apache, PHP, mysql
- Starts and enables httpd, mysql 
- Setup virtualhost in both client systems
- Copies test file content to documentroot
- Handler used to notify and restart httpd service
## Role Hirarachy
```
/lamp-linux/files = include following files
apache.conf.j2, info.php.j2, test.html , test.php.
```
```
/lamp-linux/handler = it include main.yml file it includes code for restart services
```
```
/lamp-linux/task = it include following files main.yml file is targeting to other file as per OS family
 Debian.yml  RedHat.yml  main.yml
```
```
/lamp-linux/templates - it includes following templates.
 apache.conf.j2 , httpd.conf.tmpl , info.php.j2 ,vhost.conf.tmpl
```
```
/lamp-linux/vars = this include following files this file contain variable accourding to OS family
Debian.yml and RedHat.yml
```
```
/lamp-linux/test = it inludes inventory file and main file which calling to role
```
## How to use?

To begin with this project, first ensure that ansible is installed on your server.

First create your Inventory file. You can work entirely in this repository. Name your Inventory file and setup all required connections there.

Example Inventory file:
```
[example-host]
xxx.xxx.xxx.xxx

[example-host]
xxx.xxx.xxx.xxx 
```

Next setup your playbook. Here I have setup my playbook main-role.yml and included roles for Devops Internal Ansible  on both the clients. For the execution of the playbook, first check the connection status to your client servser via:

```sh
ansible  -m ping [server ip]
```
Once you have established the connection then check for any syntax error in the playbook:

```sh
ansible-playbook  YOUR_PLAYBOOK_FILE.yml --syntax-check
```

if all checks have pass then you are good to execute the ansible-playbook:

```sh
ansible-playbook  YOUR_PLAYBOOK_FILE.yml
```
After Ansible deployment, login to the client servers and check if everything is as good as it was planned.
list php version available for linux

The availability of different PHP versions for Linux depends on the distribution you are using.

As of my knowledge cutoff (2021), the following PHP versions are available for various Linux distributions:

PHP 8.0: This is the latest version of PHP, and includes many new features and improvements, such as named arguments, attributes, and improved type declarations.

PHP 7.4: This is a previous version of PHP that is widely used in production environments. It includes many features and improvements over previous versions, such as improved type hints and typing, new features for developers, and improved performance.

PHP 7.3: This is an older version of PHP that is no longer actively maintained, but may still be in use in some environments.

PHP 7.2: This is an older version of PHP that is no longer actively maintained, but may still be in use in some environments.

Note: The availability of different PHP versions may vary depending on the Linux distribution you are using. It is always a good idea to consult the official PHP documentation for the latest information.




ashwini jachak
list php version available for ubuntu
!
The availability of different PHP versions for Ubuntu depends on the version of Ubuntu you are using and the repositories you have configured.

As of my knowledge cutoff (2021), the following PHP versions are available for Ubuntu:

PHP 8.0: This version is included in the official Ubuntu 20.04 LTS (Focal Fossa) repository and can be installed using the apt package manager.

PHP 7.4: This version is available in the official Ubuntu 20.04 LTS (Focal Fossa) repository and can be installed using the apt package manager.

PHP 7.3: This version is available in the official Ubuntu 18.04 LTS (Bionic Beaver) repository and can be installed using the apt package manager.

PHP 7.2: This version is available in the official Ubuntu 16.04 LTS (Xenial Xerus) repository and can be installed using the apt package manager.

