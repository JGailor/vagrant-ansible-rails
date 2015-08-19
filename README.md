# Overview
This is a simple Vagrant configuration and an Ansible provisioning playbook that can be used to setup a Rails environment on a VM in your local environment for development and testing.  Once you've launched the VM using the ```vagrant up``` command, you can then use ```vagrant ssh``` to connect to the system and start development and testing, while doing all of your editing using your text editor on your host environment.  Once you are ready to build staging, production, etc. environments, switch to using the ```ansible-playbook``` command with an appropriate inventory file for that environment, and you will have a system up and running quickly.

## Usage
1. Copy the following files/directories to your Rails app folder
  * ```/roles``` directory
  * ```rails_server.yml```
  * ```Vagrantfile```
2. Run ```vagrant up```, and wait for the VM to start and the system to be provisioned.
3. Run ```vagrant ssh```, and ```cd /vagrant```.
4. Open a browser, and point it to ```http://192.168.66.66```
  * Changed this by editing the line ```machine.vm.network "private", ip: "192.168.66.66")``` in the ```Vagrantfile``` to whatever IP address you want to use for the private network.
5. Open your text editor to your Rails app directory on your host machine (laptop, desktop, whatever) and start editing.
6. Reload the page in your browser and you should see the updates.
  * Standard "I need to restart Rails because of this change" items still apply.
  * Restart the server by doing ```%> touch tmp/restart.txt``` from the command line in the ```/vagrant``` folder on the VM.

## To-Dos
1. Add documentation for multi-box setup, specifically targeted to running a second VM for the database server

2. Re-evaluate whether or not ```/roles/ruby``` shouldn't be rolled into another role

## FAQS
- Where can I go learn about this Ansible bullshit?
  - [Ansible Docs](https://docs.ansible.com/ansible/index.html)

## Project Layout
```bash
.
+-- roles
|   +-- common
|   |   +-- tasks
|   |   |   +-- main.yml
|   +-- mysql
|   |   +-- tasks
|   |   |   +-- main.yml
|   +-- ruby
|   |   +-- tasks
|   |   |   +-- main.yml
|   +-- webapp
|   |   +-- tasks
|   |   |   +-- main.yml
+-- .gitignore
+-- rails_server.yml
+-- README.md
+-- Vagrantfile
```

`./roles`: Standard layout for Ansible roles for the playbook.  Each role represents some logical need of the system, such as what it requires to be a webapp, or what it requires to be a database server.

`./roles/common`: Role that should be run on every server being configured.

`./roles/mysql`: Role for setting up a mysql server.

`./roles/mysql/tasks/main.yml`: Tasks for setting up a mysql server.

`./roles/ruby`: A questionable choice. Role for setting up Ruby on a server.

`./roles/ruby/tasks/main.yml`: Tasks for setting up Ruby with ruby-install on a server.

`./roles/webapp`: Role for setting up a webapp server.  Might be renamed to `/roles/rails`.

`./roles/webapp/tasks/main.yml`: Tasks for setting up a Rails webapp server with passenger + nginx

`./roles/webapp/templates`: Templates the webapp role needs to build files on the server.  My preference is to have the directory structure under the ```/templates``` folder mirror the filesystem on the server, so a developer or ops person can immediately understand where a template will be rendered t.

`./.gitignore`: Here we want to make sure we do not check-in the ```./vagrant``` folder which is where we store the state of the running vm

`./rails_server.yml`: The playbook to build and setup a Rails server

`./README.md`: This document

`./Vagrantfile`: The configuration for Vagrant to run a local virtual machine.