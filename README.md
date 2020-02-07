# Lab 50: Prerequistes 



## Creating an Oracle on-premise environment
This directory contains Vagrant build files to provision an Oracle Database automatically, using Vagrant, an Oracle Linux 7 box and a shell script.(space, space)

1. Install [Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)
2. Install [Vagrant](https://vagrantup.com/)
3. Clone the vagrant-boxes repository `git clone https://github.com/oracle/vagrant-boxes`
2. Change into the desired version folder
3. Download the installation zip files from OTN into this folder - first time only:
[http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html)
4. Run `vagrant up`
5. Connect to the database via `vagrant ssh`
6. You can shut down the box via the usual `vagrant halt` and the start it up again via `vagrant up`.

## Setting up the necessary installation procedures inside the Database instance
1. Install [JDK-8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
   - note: any JDK version 7 or higher will work, but some packages are archived on higher JDK versions such as 11 or 13
   - make sure that you install the linux x64 rpm file
2. Install the [Oracle Database Backup Module](https://www.oracle.com/database/technologies/oracle-cloud-backup-downloads.html)
3. Install the vagrant-scp plugin `vagrant plugin install vagrant-scp`
4. Move the opc_installer.zip and jdk-8u241-linux-x64.rpm file to your Oracle database directory
5. then you want to scp the two files into the database instance:

   `vagrant scp opc_installer.zip :~`
   `vagrant scp jdk-8u241-linux-x64.rpm :~`
