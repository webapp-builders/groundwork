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
*Note*: If your computer only supports 32-bit operating systems, open the file: `Vagrantfile`<br>
Comment out lines 3 and 4, and uncomment lines 6, 7 to use "precise32" (which is the operating system that will run inside VirtualBox).

---------------------------------

## Step Six


```
vagrant up
```

If you need to stop through the process for any reason (or if the recipe gets updated), please type:

```
vagrant provision
```

---------------------------------

## Step Seven

```
vagrant ssh
```

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
