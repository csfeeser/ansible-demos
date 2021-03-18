# Day 4 Challenge!

Do a fresh build of our planetexpress machines:

`wget https://labs.alta3.com/projects/ansible/deploy/max-teardown.sh && bash teardown.sh`

`wget https://labs.alta3.com/projects/ansible/deploy/pexpress-setup.sh && bash pexpress-setup.sh`

Let's put some of the skills we've learned this week to use. Create a playbook that automates SSH key distribution, generates logs, and makes an API call. Write a playbook that does the following:

- Collects logs!

- Connects to all planetexpress hosts

- Automate the copying of SSH keys into Linux hosts rather than using ssh-copy-id user@host (but NOT to farnsworth!)
    > Suggestion: look up the **authorized_key** module!

- **Securely** collect the ssh password for use in connection to farnsworth.
    > DO NOT collect a log on this task!

- Save NASA's Astrological Picture of the Day (APOD) from the following link to each planetexpress host in a directory called `astronomy`.

    `https://www.nasa.gov/sites/default/files/thumbnails/image/apod.jpg` 
