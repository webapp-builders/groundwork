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
**_`vagrant provision` may be used for two reasons_**:<br>
A. If for any reason, you had stopped through the process and want to continue where you left off.<br>
B. If you update your ansible recipe, and you want to update your virtual machine.

**_Terminal Message 3_**: You may receive this error if your vagrant version is older than version 1.5.4 <br>
To check type `vagrant -v` in your terminal. <br> <br>To fix it; update your vagrant and run `$ vagrant up ` again.

```
Bringing machine 'default' up with 'virtualbox' provider...
There are errors in the configuration of this machine. Please fix
the following errors and try again:

vm:
* The box 'ubuntu/trusty64' could not be found.
```
---------------------------------

## Step Seven

```
vagrant ssh
```

Your terminal prompt should change from your normal one.

**For example**:<br>
(These are not exact, the will vary from computer to computer)<br>
Your terminal prompt _before_:   OSX@jennifer~/myworkfiles $<br>
Your terminal prompt _after_:   vagrant@vagrant-ubuntu-trusty-64:~$<br>

Once you have typed `vagrant ssh` and your terminal prompt has successfully changed to a new one such as `vagrant@vagrant-ubuntu-trusty-64:~$` this means you are now **using the terminal of another operating system!**

The whole reason you are using Vagrant is to have another operating system (within your computer) to have a completely isolated environment for development.  

---------------------------------

Type `cd /vagrant`. This will put you in your virtual machine's **_Shared Directory_**. <br>
(See "Understanding Shared Directories" below):

### If you want to use your own application (like from Hartl's www.RailsTutorial.org, for example) this is a good place to start.

**_For example:_**<br>
(This is only one way to do it.  Similar to Hartl's tutorial in Section 1.3).<br>
Once you are in the `/vagrant` directory, you could:
* Install Rails gem, specifying version `gem install rails -v 4.2.0.beta4`
* Create a new directory to hold all of your Rails applications `mkdir workspace`
* Move into the workspace directory `cd workspace`
* Create new Rails app, specifying version `rails _4.2.0.beta4_ new example_app`<br>
  (Hartl Section 1.3, Section 2.1, Section 3.1, etc.)
* A new Rails app should have run "bundle install" automatically, but if it did not, run `bundle install`
* Move into your new application directory `cd example_app`
* Run the rails server.   Running the rails server **_in Vagrant_** needs additional parameters (see STEP TEN).


**_Instructions needed to launch Rails server locally, while in a Vagrant remote OS:_**<br>
While in the `/vagrant` shared directory, once new application setup is complete, you may  **_skip to STEP TEN_** to launch the rails server.

---------------------------------

### Understanding Shared Directories:
(You can skip to **STEP EIGHT** if you understand how Vagrant shares directories)<br>
  
  There is now a **_SHARED DIRECTORY_** between the two operating systems.
  
  **Terminology**:<br>
  Your normal computer's OS is called: the **_host OS_**<br>
  The new computer's OS, you created in VirtualBox, is called: the **_remote OS_**

  First off, let's get our bearings.<br>

  `vagrant ssh` opened a connection between the two computers, and automatically you are now using the terminal of the remote OS. 
  
  * After you have done `vagrant ssh`
  * After the terminal prompt change to something like `vagrant@vagrant..:~$` 
  * You are now navigating the terminal of the **_remote OS_**.

Now, in the remote OS, try to list all of your files and directories, by typing `ls`.<br>
You will likely get *no results* (or only a file or two).  You *will not* see a list of directories.<br>

**Though you _did not see_ any directories, you CAN access the shared directory:<br>**
Access the shared directory by typing `cd /vagrant`<br>
  * This may feel counter-intuitive.  You just tried listing directories by tying `ls` and there were no results.
  * Still, you **_CAN CHANGE INTO THE SHARED DIRECTORY_** by typing `cd /vagrant`.
"vagrant" is the default name given to your shared directory (specified at setup).

You can think of your shared directory as a portal between two operating systems.  That means that you can access your files from two locations: (1) in your virtual machines operating system (the _remote OS_), and (2) from your normal computer(the _host OS_).

**_(1) Accessing the file through your remote OS:_** <br>
(After typing `cd /vagrant`)<br>
Once again, type `ls`.<br>
You **will see a list of directories** populated by the Groundwork project (This does not come standard. The Groundwork repo provided you with extra files and directories.  You can navigate these directories as you normal would.)  

**_(2) Access the files through your normal machine:_**<br>
In a seperate terminal (or however you usually browse through files and directories)...<br>
Go to the directory where you cloned Groundwork (from **STEP FOUR**)

#### These are the **_exact same files_** accessible from two locations.  If you edit them in one place, they are edited in the other.

The Groundwork project has seeded you with these starter directories and files.<br>
You can play with them by typing `cd /application/web` <br>
(**This is the same as STEP EIGHT**)

You are now in a rails directory.  Go to STEP NINE.

---------------------------------

## Step Eight

```
cd /vagrant/application/web
```

---------------------------------

## Step Nine

```
bundle install
rake db:create db:migrate
```

---------------------------------

## Step Ten

```
rails server -b 33.33.33.33
```

Go to your browser and open http://33.33.33.33:3000
