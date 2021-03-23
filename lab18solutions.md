Here is the solution for the looping challenge in Lab 18:

```
---
- name: Exploring the template module and jinja expressions
  hosts: planetexpress
  gather_facts: no 

  vars_files:
    - vars/planetexpress.yml

  tasks:
    - name: Configure spaceship registration
      template: 
        src: templates/ship.cfg.j2   
        dest: ~/ship.cfg            
        
    - name: Configure mission orders
      template:
        src: templates/mission-orders.txt.j2
        dest: ~/{{ item.mission }}-mission-orders.txt   
        #loop: [{"mission": "primary", "planet": "luna park"}, {"mission": "secondary", "planet": "cineplex 14"}]
      loop:
       - mission: primary
         planet: luna park
       - mission: secondary
         planet: cineplex 14
```

And you'd also need to edit the jinja2 template as well to this:

```
Good news, {{ ansible_user }}! We have another mission to accomplish:

{% if item.planet|lower == "luna park" %}
Delivery to Luna Park
Contents: Prizes for the claw crane
Delivery at: Luna Park, Moon

{% elif item.planet|lower == "cineplex 14" %}
Delivery to Cineplex 14
Contents: Popcorn
Delivery at: Cineplex 14

{% elif item.planet|lower == "omicron persei 8" %}
Delivery to Omicron Persei 8
Contents: Candy hearts
Delivery at: Omicron Persei 8

{% else %}
Delivery to Earth
Contents: R&R / Time Off
Delivery at: HQ
{% endif %}
```
