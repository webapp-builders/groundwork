# README - Installation Instructions

---------------------------------

## Step Zero - Install Ansible

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

## Step One - Virtualbox

Download [VirtualBox](https://www.virtualbox.org/wiki/Downloads) and install.

---------------------------------

## Step Two - Vagrant

Download [Vagrant](http://www.vagrantup.com/downloads) and install.
+ we recommend Starting with [rails/rails-dev-box](https://github.com/rails/rails-dev-box)

---------------------------------

## Step Three - Repo

```
git clone https://github.com/webapp-builders/groundwork.git
```

---------------------------------

## Step Four

```
cd groundwork
```

---------------------------------

## Step Five

```
vagrant up
```

If you need to stop through the process for any reason (or if the recipe gets updated), please type:

```
vagrant provision
```

---------------------------------

## Step Six

```
vagrant ssh
```

---------------------------------

#### If you want to use your own application (like the hartl tutorial, for example), do the necessary steps you do and skip to step 10.

---------------------------------

## Step Seven

```
cd /vagrant/application/web
```

---------------------------------

## Step Eight

```
bundle install
```

---------------------------------

## Step Nine

```
bundle exec rspec spec
```

---------------------------------

## Step Ten

```
rails server -b 33.33.33.33
```

Go to your browser and open http://33.33.33.33:3000
