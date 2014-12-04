# README - Installation Instructions

---------------------------------

## Step Zero - Install Ansible

$ sudo easy_install pip
$ sudo pip install ansible

### OR (if you have homebrew)

$ brew install ansible

---------------------------------

## Step One - Virtualbox

Download [VirtualBox](https://www.virtualbox.org/wiki/Downloads) and install.

---------------------------------

## Step Two - Vagrant

Download [Vagrant](http://www.vagrantup.com/downloads) and install.

---------------------------------

## Step Three - Repo

$ git clone https://github.com/webapp-builders/groundwork.git

---------------------------------

## Step Four

$ cd groundwork

---------------------------------

## Step Five

$ vagrant up

---------------------------------

## Step Six

$ vagrant ssh

---------------------------------

## Step Seven

$ cd /vagrant

---------------------------------

## Step Eight

$ bundle install

---------------------------------

## Step Nine

$ bundle exec rspec spec
