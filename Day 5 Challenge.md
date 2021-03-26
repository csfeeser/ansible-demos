# Day 5 Challenge

### Running against [planetexpress], write a playbook that does the following:

1. Stores the value of `ansible_ssh_pass` inside Ansible Vault.

0. Has a precheck that confirms the following:
   - `https://api.nasa.gov/planetary/apod?api_key=tFXI8wD5RLHE84WEvtZg8MdkychOZn0bV4T6sgM4` is a valid URL.
   - That the string "video" is NOT inside this API response! If it does, trigger an error that returns the message- "APOD url is a video, not an image."

0. Display what the value of `url` is in this API response.

0. Save the image returned by `url` as a file in each host's home directory.
