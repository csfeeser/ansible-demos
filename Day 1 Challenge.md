# Day 1 Content Challenge!

I hope yesterday was educational and engaging for you all! To test what you've learned, please do the following:

- 1. Create a new hosts file called `challenge`. Add the following to it:

```
[renamed]
bugs      ansible_host=10.10.2.3 ansible_user=bender ansible_python_interpreter=/usr/bin/python3
daffy         ansible_host=10.10.2.4 ansible_user=fry ansible_python_interpreter=/usr/bin/python3
elmer    ansible_host=10.10.2.5 ansible_user=zoidberg ansible_python_interpreter=/usr/bin/python3
taz  ansible_host=10.10.2.6 ansible_user=farnsworth ansible_ssh_pass=alta3
```

- 2. Write a playbook that includes the following:
    - explicitly states there will be an ssh connection to the hosts
    - writes to all hosts in `renamed` EXCEPT for *taz*.
    - DO NOT gather facts about your hosts
    - Create vars that have a value of *your name* 
    - Create a new user with *your name* in each machine. Assign it the group *funkytown*
