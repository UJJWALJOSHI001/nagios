# nagios
  nagios setup on localhost

# Step 1: Install Prerequisite Software.
    #sudo yum install httpd php 
    #sudo yum install gcc glibc glibc-common 
    #sudo yum install gd gd-devel 

# Step 2: Create Account Information
 
    #sudo adduser -m nagios 
    #sudo passwd nagios  
 
 ## GROUP ADD 
     
    #sudo groupadd nagcmd 
    #sudo usermod -a -G nagcmd nagios 
    #sudo usermod -a -G nagcmd apache 


# Step 3: Download Nagios Core and the Plugins
    
    #mkdir ~/downloads
    
    #cd ~/downloads
  
    #wget http://prdownloads.sourceforge.net/sourceforge/nagios/nagios-4.0.8.tar.gz
  
  
    #wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz
  
# Step 4: Compile and Install Nagios
   
    #tar zxvf nagios-4.0.8.tar.gz
    
    #cd nagios-4.0.8

 ## Run the configuration script with the name of the group which you have created in the above step.
  
  
    #./configure --with-command-group=nagcmd
   
 ## Compile the Nagios source code


    #make all
 
 
 
 ## Install binaries, init script, sample config files and set permissions on the external command directory.


    #sudo make install


    #sudo make install-init


    #sudo make install-config

 
    #sudo make install-commandmode

# Step 5: Customize Configuration

 
 ## Change E-Mail address with nagiosadmin contact definition you’d like to use for receiving Nagios alerts.


    #sudo vim /usr/local/nagios/etc/objects/contacts.cfg



# Step 6: Configure the Web Interface

    #sudo make install-webconf


## Create a nagiosadmin account for logging into the Nagios web interface. Note the password you need it while login to Nagios web console

    #sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin  ## type password

    #systemctl restart httpd


# Step 7: Compile and Install the Nagios Plugins

## Extract the Nagios plugins source code

    #cd ~/downloads


    #tar zxvf nagios-plugins-2.0.3.tar.gz


    #cd nagios-plugins-2.0.3

## Compile and install the plugins.

    #./configure --with-nagios-user=nagios --with-nagios-group=nagios


    #make

    #make install
 
# Step 8: Start Nagios


    #chkconfig --add nagios

    #chkconfig nagios on

## Verify the sample Nagios configuration files.


    #/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg

# step 9: Start Nagios service

 
    #systemctl start nagios
 
# Step 10: Log in to the Web Interface
   
     access the Nagios web interface to do this you will need to know the Public DNS or IP or your Private IP 
     
     You’ll be prompted for the username (nagiosadmin) and password you specified earlier.

    e.g. http://IP/nagios/

