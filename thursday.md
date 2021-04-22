# HTTP UFW Challenge

Write a playbook that installs the following applications on ALL our **planetexpress** machines, which are a combination of Debian & RedHat (CentOS) hosts. The problem is the steps are DIFFERENT depending on the operating system you are targeting! Your goal is to write a playbook that does the following:

1. Install Apache webserver
    - debian / ubuntu: `sudo apt install apache2`
    - redhat / centos: `sudo yum install httpd`

0. Install some uncomplicated firewall rules
    - debian / ubuntu: `sudo apt install ufw`
    - redhat / centos: `yum install -y epel-release` AND `sudo yum install ufw`

0. Push a new mock config file (generated from a template) to...
    - debian / ubuntu: "/etc/apache2/apache2.conf"
    - redhat / centos: "/etc/httpd/conf/httpd.conf"

0. ONLY if services were installed or if configuration files were pushed, restart the services.
