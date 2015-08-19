# Overview
This is a simple Vagrant configuration and an Ansible provisioning playbook that can be used to setup a Rails environment on a VM in your local environment for development and testing.  Once you've launched the VM using the ```vagrant up``` command, you can then use ```vagrant ssh``` to connect to the system and start development and testing, while doing all of your editing using your text editor on your host environment.  Once you are ready to build staging, production, etc. environments, switch to using the ```ansible-playbook``` command with an appropriate inventory file for that environment, and you will have a system up and running quickly.

# Usage
1. Copy the ```roles``` directory, the ```rails_server.yml``` file, and ```Vagrantfile``` file to you Rails app directory.
2. Run ```vagrant up```, and wait for the VM to start and the system to be provisioned.
3. Run ```vagrant ssh```, and ```cd /vagrant```.
4. Open a browser, and point it to ```http://192.168.66.66``` (this can be changed by editing the line ```machine.vm.network "private", ip: "192.168.66.66")``` in the ```Vagrantfile``` to whatever IP address you want to use for the private network.
5. Open your text editor to your Rails app directory on your host machine (laptop, desktop, whatever) and start editing.
6. Reload the page in your browser and you should see the updates.  Standard "I need to restart Rails because of this change" items still apply, but you can restart the server by doing ```%> touch tmp/restart.txt``` from the command line in the ```/vagrant``` folder on the VM.