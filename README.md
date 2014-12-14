# README - Installation Instructions

---------------------------------

## Step One - Install Ansible

You can follow the instructions on the [Ansible website](http://docs.ansible.com/intro_installation.html#installing-the-control-machine) or either of the options below:

```
sudo easy_install pip
sudo pip install ansible
```

### OR (if you have OSX homebrew)

```
brew install ansible
```

### OR (if you use ubuntu/debian)

```
sudo apt-get install python-yaml python-markupsafe nfs-kernel-server nfs-common portmap
sudo apt-get install software-properties-common
```
Test to see if ansible is installed using `ansible --version`  If it is not installed, do the following:
```
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
```

### OR (if you have centos/redhat)

```
yum install ansible
```

---------------------------------

## Step Two - Virtualbox

Download [VirtualBox](https://www.virtualbox.org/wiki/Downloads) and install.

---------------------------------

## Step Three - Vagrant

Download [Vagrant](http://www.vagrantup.com/downloads) and install.

---------------------------------

## Step Four - Repo

Go to directory you want clone into. For example, if you want to clone into `/someuser/myapps/`

You could do: `cd /someuser/myapps/`

Then type below:
```
git clone https://github.com/webapp-builders/groundwork.git
```

---------------------------------

## Step Five

```
cd groundwork
```

You can confirm that you are in the correct directory by typing `ls`.<br>
If you see a file `Vagrantfile` you are in the correct directory.

**_Note_**: If you are using ubuntu as your primary OS, uncomment line 22 to use the VirtualBox GUI.

**_Note_**: If your computer only supports 32-bit operating systems, after `cd groundwork`, open the file: `Vagrantfile`<br>
Comment out line 3 and uncomment line 5 to use "ubuntu/trusty64" <br>
(this will tell VirtualBox to run the "precise32" operating system).

---------------------------------

## Step Six

```
vagrant up
```
**__READ Below for possible "terminal messages":__**<br>
Numerous messages and errors may occur once typing `vagrant up`.<br>
Read the following _Terminal Message 1_ and _Terminal Message 2_, to make sure you are on the right track. 

---------------------------------

**_Terminal Message 1_**:  If your terminal seems to be "stuck" at `TASK: rvm...` just wait.  This might take a while, because you are installing Ruby using RVM.  This is a good sign.  It means everything is installing properly.


**_Terminal Message 2_**:  You many receive an error if you already have Rail or Postgresql running on your machine. <br>
This means you need to *stop* Rails and/or Postgresql.

An error might look like the following:
```
Vagrant cannot forward the specified ports on this VM, since they
would collide with some other application that is already listening
on these ports. The forwarded port to 5432 is already in use
on the host machine.

To fix this, modify your current projects Vagrantfile to use another
port. Example, where '1234' would be replaced by a unique host port:

  config.vm.network :forwarded_port, guest: 5432, host: 1234

Sometimes, Vagrant will attempt to auto-correct this for you. In this
case, Vagrant was unable to. This is usually because the guest machine
is in a state which doesn't allow modifying port forwarding.
```
For Rails server, find the terminal window that is running Rails locally and press `ctrl+c` together.

You may not realize it, but Postgres might have started automatically at startup.  
If Postgresql is running, to stop your:

**_For Ubuntu_**:
```
sudo service postgresql stop
```

**_For  OSX homebrew_**:<br>
Go online, search for "how to stop postgresql osx"<br>
(There will be different instructions depending on how your Mac is setup).

---------------------------------

(You may skip this command for a first time install)<br>
Upon subsequent updates, you may want to use:
```
vagrant provision
```
**_"vagrant provision" may be used for two reasons_**:<br>
A. If for any reason, you had stopped through the process and want to continue where you left off.<br>
B. If you update your ansible recipe, and you want to update your virtual machine.


---------------------------------

## Step Seven

```
vagrant ssh
```

Your terminal prompt should change from your normal one.  

---------------------------------

#### If you want to use your own application (like the hartl tutorial, for example), do the necessary steps you do and skip to step 10.

---------------------------------

## Step Eight

```
cd /vagrant/application/web
```

---------------------------------

## Step Nine

```
bundle install
```

---------------------------------

## Step Ten

```
rails server -b 33.33.33.33
```

Go to your browser and open http://33.33.33.33:3000
