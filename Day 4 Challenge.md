# Day 4 Challenge!

### Setup:

Do a fresh build of our planetexpress machines. Here's a bash script to automate the process.

    `student@bchd:~$` `cd`
    
    `student@bchd:~$` `vim setup.sh`
    
    ```
    wget https://labs.alta3.com/projects/ansible/deploy/max-teardown.sh
    bash max-teardown.sh
    wget https://labs.alta3.com/projects/ansible/deploy/pexpress-setup.sh
    bash pexpress-setup.sh
    ssh-copy-id bender@10.10.2.3 -f
    ssh-copy-id fry@10.10.2.4 -f
    ssh-copy-id zoidberg@10.10.2.5 -f
    ```
    
    `student@bchd:~$` `bash setup.sh`

When prompted, type `alta3` as the password for bender, fry, and zoidberg.

### Challenge:

Let's put some of the skills we've learned this week to use. Create a playbook that automates SSH key distribution, generates logs, and makes an API call. Write a playbook that does the following:

- Collects logs!

- Connects to all planetexpress hosts

- Automate the copying of SSH keys into Linux hosts rather than using ssh-copy-id user@host (but NOT to farnsworth!)
    > Suggestion: look up the **authorized_key** module!

- **Securely** collect the ssh password for use in connection to farnsworth. Don't rely on the password set in our inventory file.

- Save NASA's Astrological Picture of the Day (APOD) from the following link to each planetexpress host in a directory called `astronomy`.

    `https://www.nasa.gov/sites/default/files/thumbnails/image/apod.jpg` 

<details>
<summary>SOLUTION</summary>
<br>

    - name: copy keys into remote hosts
      hosts: planetexpress

      vars_prompt:
        - name: ansible_ssh_pass
          private: yes

      tasks:
      - name: Set authorized key taken from file
        become: yes
        authorized_key:
          user: "{{ ansible_user }}" # name of the user we SSH into the system as
          state: present
          key: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}" # public key on the controller
        when: ansible_distribution == "Ubuntu"

      - name: create astronomy directory
        file:
          path: "/home/{{ ansible_user }}/astronomy/"
          state: directory

      - name: get APOD
        get_url:
          url: https://www.nasa.gov/sites/default/files/thumbnails/image/apod.jpg
          dest: "/home/{{ ansible_user }}/astronomy/"
    
</details>
