# About Vagrant

## Vagrant Commands

`vagrant up`

Starts the server. This command only works when you are in the *groundwork* directory... the same directory as the Vagrantfile.

`vagrant halt`

Stops the server

`vagrant suspend`

Server is suspended, but still running in the background.

`vagrant ssh`

Enters the server

`exit`

Exits from vagrant ssh

`vagrant status`

Shows you if vagrant is running/not running if you forgot.

`vagrant global-status`

Shows you the status of all vagrant servers that exist on your computer.

`vagrant provision`

Vagrant will look for new settings/configuration in Vagrantfile and apply it. Vagrant must be running.

`vagrant destroy`

Deletes the virtual machine. The next time you use *vagrant up*, the server will be completely rebuilt. 
This is not something you regularly do once vagrant is working correctly.


## Synced Folders
Vagrant has the ability to sync folders in the host machine with folders in the virtual machine. 

The groundwork vagrant configuration currently syncs the 'groundwork' folder in the host machine as '/vagrant' in the virtual machine.
This means if you add a folder to 'groundwork', you will see it in' /vagrant' and vice versa.

Example: '/your_name_here/groundwork/newfolder' can be found as '/vagrant/newfolder' in the virtual machine.


## Starting Rails
The default ip address used by the groundwork virtual server is:
33.33.33.33

Remember to set the ip address when you start the rails server for any project running within this virtual machine.

`rails s -b 33.33.33.33`


## Further Customization
**Changing the Vagrantfile**

If you choose to change the Vagrantfile to change the ip address of the virtual server, edit/sync additional folders, be sure to restart the Vagrant server.

```
vagrant halt
vagrant up
```

If you change the server configuration contained in the ansible directory, remember to provision the server.
`vagrant provision`


**Symbolic Link**

You can make a symbolic link if you'd like to see the folder as soon as you ssh into vagrant. It's nice but not necessary.
If you would like your new folder to be named 'workspace', start terminal and do the following:

```
cd groundwork                       # this will vary depending on where you have put the groundwork folder
mkdir workspace                     # make a new folder named workspace
vagrant up                          # start vagrant
vagrant ssh                         # enter vagrant
ln -s /vagrant/workspace workspace  # make a symbolic link named' workspace' that acts as a shortcut to '/vagrant/workspace'
exit                                # leave vagrant
vagrant halt                        # turn off vagrant, since I'm not doing anything else.
```


## Definitions
**Host machine (box/computer)**

This is the computer that Vagrant is installed on. A host machine can run more than one virtual machine. 

**Guest virtual machine (box/computer)**

This is the virtual computer that you start using vagrant. Different projects can run inside of one virtual machine OR you can have a different virtual machine for different projects.

**Vagrantfile**

This contains the configuration for the Vagrant virtual machine. It can refer to and use ansible, puppet, chef for more configuration settings.
