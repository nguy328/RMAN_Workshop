# Lab 50: Prerequistes 
Works as of 2/6/2020


## Creating an Oracle on-premise environment
This directory contains Vagrant build files to provision an Oracle Database automatically, using Vagrant, an Oracle Linux 7 box and a shell script.(space, space)

1. Install [Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)
2. Install [Vagrant](https://vagrantup.com/)
3. Clone the vagrant-boxes repository `git clone https://github.com/oracle/vagrant-boxes`
2. Change into the desired version folder
3. Download the installation zip files from OTN into this folder - first time only:
[http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html)<br />
   [IMAGE TO SHOW THE NECESSARY FILES AND SHOW THE PRE-DOWNLOADED VAGRANT FILE]<br />
4. Run `vagrant up`
5. Connect to the database via `vagrant ssh`
6. You can shut down the box via the usual `vagrant halt` and the start it up again via `vagrant up`.

## Retrieving and loading the necessary packages to the Database instance
1. Install [JDK-8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
   - note: any JDK version 7 or higher will work, but some packages are archived on higher JDK versions such as 11 or 13
   - make sure that you install the linux x64 rpm file <br />
   [IMAGE TO SHOW THE JDK-8 FILE NEEDED]<br />
2. Install the [Oracle Database Backup Module](https://www.oracle.com/database/technologies/oracle-cloud-backup-downloads.html)
3. Install the vagrant-scp plugin `vagrant plugin install vagrant-scp`
4. Move the opc_installer.zip and jdk-8u241-linux-x64.rpm file to your Oracle database directory <br />

   `mv ~/downloads/opc_installer.zip ~/downloads/jdk-8u241-linux-x64.rpm ~/vagrant-boxes/OracleDatabase/12.1.0.2`<br />
   [IMAGE TO SHOW THE MOVED FILES]</br>
5. then you want to scp the two files into the database instance: <br />
   `vagrant scp opc_installer.zip jdk-8u241-linux-x64.rpm :~`
6. Connect to the database with `vagrant ssh`
7. Check to see if the two files are there


# Lab 100: Configuring and using RMAN


##  Install the packages inside the Database instance
1. run `su` to login to the root user 
2. install the JDK with `$ rpm -ivh jdk-8u241-linux-x64.rpm`
3. Check to see if java was installed properly with `$ java -v`
4. Unzip the opc_installer.zip file via `$ unzip opc_installer.zip`
5. Get to the opc installer directory via `$ cd opc_installer`
6. there are two folders inside <br />
   [IMAGE TO SHOW THE CONTENTS OF opc_installer]<br />
7. We will use the oci_installer this time so run `$ cd oci_installer`
8. There should be a jar file called oci_install.jar `$ ls`
9. Move that to the root directory, for example `$ mv oci_install.jar /opt`
10. Then get to that directory with `$cd /opt`
11. Check whether the file is there `$ ls`<br />
    [IMAGE TO SHOW THE JAR FILE]<br />
12. There are several prereqs to run this jar file
      - hostname
      - private key
      - public key fingerprint
      - tenancy OCID
      - compartment OCID
      - user OCID
      - bucketname (optional)
      - wallet directory location (optional)
      - library directory location (optional)
      - configfile directory location (optional)
      - Also to make this work you need tenancy-level access to Object Storage, can easily be done with admin access or you can create a policy that limits access to just the required resources<br />
      
      
      Allow group <group_name> to manage objects in compartment <compartment_name> where target.bucket.name = '<bucket_name>'

      Allow group <group_name> to read buckets in compartment <compartment_name>
      
      
