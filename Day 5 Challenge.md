# Day 5 Challenge

### Running against [planetexpress], write a playbook that does the following:

1. Stores the value of `ansible_ssh_pass` inside Ansible Vault.

0. Has a precheck that confirms the following:
   - https://api.nasa.gov/planetary/apod?api_key=tFXI8wD5RLHE84WEvtZg8MdkychOZn0bV4T6sgM4 is a valid URL.
   - That the string "youtube" is NOT inside this API response! If it does, trigger an error that returns the message- "APOD url is a video, not an image."

0. Display what the value of `url` is in this API response.

0. Save the image returned by `url` as a file in each host's home directory.

### Testing:

- To test your precheck, use the following URL (which does have a YouTube video as the APOD): https://api.nasa.gov/planetary/apod?api_key=tFXI8wD5RLHE84WEvtZg8MdkychOZn0bV4T6sgM4&date=2020-09-29

<details>
<summary>SOLUTION</summary>
<br>
   
`student@bchd:~$` `cd`

`student@bchd:~$` `echo "ansible_ssh_pass: alta3" > passfile.yml`

`student@bchd:~$` `ansible-vault encrypt passfile.yml --ask-vault-pass`

`student@bchd:~$` `vim challenge5solution.yml`

```
- name: Ansible and RESTful interfaces
  hosts: planetexpress
  gather_facts: false

  vars:
    astros: https://api.nasa.gov/planetary/apod?api_key=tFXI8wD5RLHE84WEvtZg8MdkychOZn0bV4T6sgM4

  vars_files:
    - pass.yml

  tasks:
    - name: PRECHECK
      block:

      - uri:
          url: "{{ astros }}"
          return_content: yes
        register: resp
        failed_when: "'youtube' in resp.content"

      rescue:
      - fail:
         msg: "APOD url is a video, not an image."

    - name: APOD url display
      debug:
        var: resp.json.url

    - name: Download image
      get_url:
        url: "{{ resp.json.url }}"
        dest: ~/apodtest.jpg
```

`student@bchd:~$` `ansible-playbook challenge5solution.yml --ask-vault-pass`

Test against a URL that contains "youtube" in the response:

`student@bchd:~$` `ansible-playbook challenge5.yml -e "astros=https://api.nasa.gov/planetary/apod?api_key=tFXI8wD5RLHE84WEvtZg8MdkychOZn0bV4T6sgM4&date=2020-09-29" --ask-vault-pass`

</details>
