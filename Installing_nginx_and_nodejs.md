
`sudo ansible web -m ping`

`sudo nano hosts`

`ec2-instance ansible_host=34.244.24.173 ansible_user=ubuntu ansible_ssh_private_key_file=/home/ubuntu/.ssh/tech254.pem
# sudo chmod 400 tech254.pem`



Create new script to install ngin: `sudo nano install-nginx.yml`

Copy and paste

``` 
create a playbook to provision ngin web server in web-node
---
#starts with thee dashes
# where do you want to install or run this playbook
- hosts: web

# find the facts
  gather_facts: yes

# provide admin access to this playbook
  become: true

# provide the actual instructions - instal nginx
  tasks:
  - name: provision/install/configure Nginx
    apt: pkg=nginx state=present

# ensure nginx is running/enabled
```

Run the script: `sudo ansible-playbook install-nginx.yml`

Create new script to install nodeJS: `sudo nano install-nodejs.yml`

```
---
# where do you want to install or run this playbook
- hosts: web

# find the facts
  gather_facts: yes

# provide admin access to this playbook - use sudo
  become: true

# provide the actual instructions - install NodeJS
  tasks:
  - name: Install the NodeSource Node.js 12.x release PPA
    shell: "curl -sL https://deb.nodesource.com/setup_12.x | bash -"

  - name: Install Node.js
    apt: pkg=nodejs state=present

  - name: Check Node.js version
    shell: "node -v"
    register: node_version

  - name: Display Node.js version
    debug:
      msg: "Node.js version is {{ node_version.stdout }}"

  - name: Check NPM version
    shell: "npm -v"
    register: npm_version

  - name: Display NPM version
    debug:
      msg: "NPM version is {{ npm_version.stdout }}"
```

Run the script: `sudo ansible-playbook install-nodejs.yml`

Should out the below:

![](\Screenshots\install_nodejs.png)

