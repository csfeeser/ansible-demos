# Day 5 Challenge!

### Setup:

Do a fresh build of our planetexpress machines. Here's a bash script to automate the process.

`student@bchd:~$` `cd`
    
`student@bchd:~$` `vim setup.sh`
    
    wget https://labs.alta3.com/projects/ansible/deploy/max-teardown.sh
    bash max-teardown.sh
    wget https://labs.alta3.com/projects/ansible/deploy/pexpress-setup.sh
    bash pexpress-setup.sh
    ssh-copy-id bender@10.10.2.3 -f
    ssh-copy-id fry@10.10.2.4 -f
    ssh-copy-id zoidberg@10.10.2.5 -f
    
`student@bchd:~$` `bash setup.sh`

When prompted, type `alta3` as the password for bender, fry, and zoidberg.

### Challenge:

Let's put some of the skills we've learned this week to use. Create a playbook that does the following:

- Automate ensuring that the `max-teardown.sh` and `mod-setup.sh` bash scripts are in the `/home/student` directory!

- Have Ansible execute `max-teardown.sh` and `mod-setup.sh` (in that order, of course) on localhost.

- Automate the copying of SSH keys into Linux hosts rather than using ssh-copy-id user@host.
    > Suggestion: look up the **authorized_key** module!
    
    > Follow up suggestion... this will require a SECOND play!


<details>
<summary>SOLUTION</summary>
<br>

```yaml
---
- name: "Download/Execute Bash Scripts"
  hosts: localhost
  connection: local
  gather_facts: no
  become: yes

  tasks:

  - name: Download our bash scripts
    get_url:
      url: "{{ item }}"
      dest: "/home/student/"
    loop: ["https://static.alta3.com/projects/ansible/max_teardown.sh", "https://static.alta3.com/projects/ansible/modules/setup.sh"]

  - name: Run bash scripts
    script:
      cmd: "{{ item }}"
    loop: ["/home/student/max_teardown.sh", "/home/student/setup.sh"]

- name: "Copy Public Keys"
  hosts: planet_express,!farnsworth
  connection: ssh
  gather_facts: no
  become: yes

  vars:
    ansible_ssh_pass: alta3

  tasks:
    - name: Set authorized key taken from file
      authorized_key:
        user: "{{ ansible_user }}"
        state: present
        key: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}" # public key on the controller
```

</details>
