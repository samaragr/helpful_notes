## Setup local dev environment (Mac)
### Install VirtualBox & Vagrant
https://www.virtualbox.org/wiki/Downloads
https://sourabhbajaj.com/mac-setup/Vagrant/README.html

> brew install vagrant

#### Vagrantfile
> cd ~
> mkdir ansible
> vim Vagrantfile

```ruby
IP_NW = "192.168.33."
NODE_IP_START = 1
NUM_NODE = 2

Vagrant.configure("2") do |config|
  config.vm.box = "centos/8"

  config.vm.box_check_update = false

  (1..NUM_NODE).each do |i|
    config.vm.define "ansiblenode0#{i}" do |node|
      node.vm.hostname = "ansiblenode0#{i}"
      node.vm.network :private_network, ip: IP_NW + "#{NODE_IP_START + i}"

      node.vm.provider :virtualbox do |v|
        v.name = "ansiblenode0#{i}"
        v.memory = 1024
        v.cpus = 1
        v.linked_clone = true
      end

      node.ssh.insert_key = false
    end
  end
end
```

Startup the target Centos Linux machines
> vagrant up

Access to one of the target machine:
> vagrant ssh ansiblenode01

Logout from inside the target machine terminal:
> logout

Delete machines (optional):
> vagrant destroy

### Locate SSH private key
> vagrant ssh-config

Note down the `IdentityFile` value.

### Install Ansible on host machine (Mac)
> brew install ansible

### Ansible hosts / Inventory
Edit or create if not exists:
> vim /etc/ansible/hosts

or
> vim inventory
```
[myvirtualmachines]
node01 ansible_host=192.168.33.2 ansible_ssh_user=vagrant ansible_ssh_private_key_file=[path/to/insecure_private_key]
node02 ansible_host=192.168.33.3 ansible_ssh_user=vagrant ansible_ssh_private_key_file=[path/to/insecure_private_key]
```

The `insecure_private_key` refers to the `IdentityFile` value found above.

Note: Ansible looks up the hosts file by default. Custom inventory file can be created in individual project folder to override the default hosts.

### Test Ansible connection to target Linux machines
> ansible node01 -m ping
> ansible node02 -m ping

It should respond with SUCCESS message `pong`.

