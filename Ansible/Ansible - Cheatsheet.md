## Playbook Cheatsheet (YAML)
## Ansible Playbook
> mkdir ~/ansible/playbook
> cd ~/ansible/playbook
## Disable SSH Ansible config
> vim ansible.cfg
```
[defaults]
host_key_checking = False
```

## Inventory file

| Argument                     | Example                 |
| ---------------------------- | ----------------------- |
| ansible_host                 | node01                  |
| ansible_port                 | 22 (default)            |
| ansible_user                 | username                |
| ansible_pass                 | password                |
| ansible_ssh_private_key_file | path/to/ssh_private_key |

##### INI format
```
mail.example.com

[webservers]
foo.example.com
bar.example.com

[dbservers]
one.example.com
two.example.com
three.example.com
```
##### YAML format
```yaml
all:
  hosts:
    mail.example.com:
  children:
    webservers:
      hosts:
        foo.example.com:
        bar.example.com:
    dbservers:
      hosts:
        one.example.com:
        two.example.com:
        three.example.com:

```

## Playbook
### Run Playbook in localhost
> ansible-playbook -i localhost, playbook.yml -vv
##### Run Playbook by inventory hosts
> ansible-playbook -i inventory playbook.yml

### Playbook.yaml examples 
Use `command` module to view the content of `/etc/resolv.conf` file
```yaml
- name: Execute a command on localhost
  hosts: localhost
  connection: local
  tasks:
    - name: Execute a command
      command: cat /etc/resolv.conf
```

 Use `file` module to create empty file under a folder and change ownership to user `vagrant`
 
```yaml
---
- hosts: node01
  become: true
  tasks:
    - name: Creating blog.txt file
      file:
        path: /opt/blog.txt
        state: touch
        group: vagrant

- hosts: node02
  become: true
  tasks:
    - name: Creating story.txt file
      file:
        path: /opt/story.txt
        state: touch
        owner: vagrant
```

Use `copy` module to create a file with text content

```yaml
---
- hosts: node01
  become: true
  tasks:
    - name: create a file
      copy:
        dest: /opt/file.txt
        content: "This file is created by Ansible!"
```

Note: Use `become: true` when it is required to execute the command by sudo user.

Use `copy` module to copy file from localhost to both remote nodes
 
```yaml
---
- hosts: all
  become: true
  tasks:
    - copy:
        src:  /path/to/filename
        dest: /opt/filename
        remote_src: yes
```

Use `replace` module to replace text in file
```yaml
---
- hosts: node01
  become: true
  tasks:
    - replace:
        path: /path/to/filename
        regexp: 'Kodekloud'
        replace: 'Ansible'

- hosts: node02
  become: true
  tasks:
    - replace:
        path: /path/to/filename
        regexp: 'Ansible'
        replace: 'Kodekloud'
```

#### Conditional command
```yaml
---
- name: 'Am I a Banana or not?'
  hosts: localhost
  connection: local
  vars:
    fruit: banana
  tasks:
    - command: 'echo "I am a Banana"'
      when: fruit == "banana"

    - command: 'echo "I am not a Banana"'
      when: fruit != "banana"
```

#### Loop
```yaml
---
- name: 'Print fruits'
  hosts: localhost
  connection: local
  vars:
    fruits:
      - Apple
      - Banana
      - Grapes
      - Orange
  tasks:
    - command: 'echo "{{ item }}"'
      with_items: '{{ fruits }}'
```

Or use `loop` in latest version of Ansible
```yaml
---
- name: 'Print fruits'
  hosts: localhost
  connection: local
  vars:
    fruits:
      - Apple
      - Banana
      - Grapes
      - Orange
  tasks:
    - command: 'echo "{{ item }}"'
      loop: '{{ fruits }}'
```

Note: `with_*` is available based on the availability of the `lookup` plugin. It is recommended to use `loop` in newer Ansible versions

For example:
`with_list` is directly replaced by `loop`
```yaml
- name: with_list
  ansible.builtin.debug:
    msg: "{{ item }}"
  with_list:
    - one
    - two

- name: with_list -> loop
  ansible.builtin.debug:
    msg: "{{ item }}"
  loop:
    - one
    - two
```

`with_flatten` is replaced by `loop` and `flatten` filter
```yaml
- name: with_flattened
  ansible.builtin.debug:
    msg: "{{ item }}"
  with_flattened: "{{ items }}"

- name: with_flattened -> loop
  ansible.builtin.debug:
    msg: "{{ item }}"
  loop: "{{ items|flatten }}"
```

For details, refer to https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_loops.html#migrating-to-loop

Use `yum` module to install `vim-enhanced` package
```yaml
---
- name: 'Install the required package'
  hosts: all
  become: yes
  tasks:
    - yum: 
        name: vim-enhanced
        state: present
```

Use `copy` module to copy file to the nodes with owner, group, and permission
```yaml
---
- hosts: all
  become: true
  tasks:
    - name: Copy file with owner and permissions on node01
      copy:
        src: /usr/src/condition/blog.txt
        dest: /opt/condition/blog.txt
        owner: bob
        group: bob
        mode: "0640"
      when: inventory_hostname == "node01"

    - name: Copy file with owner and permissions on node02
      copy:
        src: /usr/src/condition/story.txt
        dest: /opt/condition/story.txt
        owner: sam
        group: sam
        mode: "0400"
      when: inventory_hostname == "node02"
```

Use `lineinfile` module Add line of text into file
```yaml
---
- hosts: node01
  become: true
  tasks:
  - lineinfile:
      path: /var/www/html/index.html
      line: 'Welcome to KodeKloud Labs!'
      state: present
      insertbefore: BOF
```

Use `service` module to manage Linux service status
```yaml
---
- hosts: all
  become: true
  tasks:
  - name: Install httpd package
    yum: name=vsftpd state=installed

  - name: Start service
    service:
      name: vsftpd
      state: started
```

Use `archive` module to create an archive (tar.gz) file
```yaml
---
- hosts: all
  become: true
  tasks:
  - name: Create an archive demo.tar.gz
    archive:
      path: /usr/src/ecommerce/
      dest: /opt/ecommerce/demo.tar.gz
```

Install `geerlingguy.nodejs` from Ansible Galaxy
> ansible-galaxy install geerlingguy.nodejs -p ~/ansible/roles

Create an Ansible role called package
> cd ~/ansible/roles
> ansible-galaxy init package

Install and start nginx
> vim ~/ansible/roles/package/tasks/main.yml
```yaml
---
# tasks file for nginx
- name: Install Nginx
  ansible.builtin.package:
    name: nginx 
    state: latest
- name: Start Nginx Service
  ansible.builtin.service:
    name: nginx 
    state: started
```

Consume the role in playbook to apply on Node01
> vim ~/ansible/role.yml
```yaml
---
- hosts: node01
  become: true
  roles:
    - roles/package
```

Run `ansible-playbook ~/ansible/role.yml` will go through the tasks specified in the role (install nginx and start the nginx service)

#### Run task2 based on the output value of task1
```yaml
---
- hosts: all
  become: true
  tasks:
    - name: Ensure Apache is at the latest version
      yum:
        name: httpd
        state: present
      register: httpd_installation_status
    - name: Ensure Apache is running
      service:
        name: httpd
        state: started
      when: httpd_installation_status.changed == True
```
Alternatively, use Ansible Handler to execute dependant tasks:
```yaml
---
- hosts: all
  become: true
  tasks:
    - name: Ensure Apache is at the latest version
      yum:
        name: httpd
        state: present
      notify: 
        - Ensure Apache is running
        - Ensure Apache status
  handler:
    - name: Ensure Apache is running
      service:
        name: httpd
        state: started
    - name: Ensure Apache status
      service:
        name: httpd
        state: status
```
