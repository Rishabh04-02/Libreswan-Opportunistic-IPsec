
# Libreswan Opportunistic IPsec Documentation


## Prerequisite
### IPsec -  [Libreswan](https://github.com/libreswan/libreswan/)
It can be installed using any of the following methods:
1. Download page official website - [https://download.libreswan.org/](https://download.libreswan.org/)
2. GitHub repository [https://github.com/libreswan/libreswan/](https://github.com/libreswan/libreswan/)
3. Using the package manager in Linux distributions:
	* Fedora - `sudo dnf -y install libreswan-3.* `
	* Centos - `sudo yum -y install libreswan-3.*`
	* Ubuntu - `sudo apt-get -y install libreswan`

Note - * refers to the latest version available.

## Installation

1. clone the [project repository](https://github.com/Rishabh04-02/Libreswan-Opportunistic-IPsec.git) using the following command:
` git clone https://github.com/Rishabh04-02/Libreswan-Opportunistic-IPsec.git`

2. Go to the project directory using the following command:
 `cd Libreswan-Opportunistic-IPsec`

 3. Run the setup file:
 `sudo bash setup`
 When you run the setup file it'll ask for: *Installing for server or client? Type (S/C)*. Choose your response accordingly.

## Sample Installation output

### For Client

        $ sudo bash setup
        [sudo] password for user:
            
        Checking if the script is run as root.
        This script is run as root. Good to go. 
        
        Installing for server or client? Type (S/C) c
        Checking if IPsec is installed
        IPsec is installed. 
        
        Downloading the letsencrypt certificates
        Deleting the certs directories certs/CA , certs/intermediate (if previously present)
        CA Certificates downloaded.
        Intermediate Certificates downloaded. 
        
        Initializing the nss database
        NSS database already initialised - aborted
        To wipe the old NSS database, issue: rm /etc/ipsec.d/*.db
        
        Importing the downloaded certificates into NSS Database
        CA certificates Imported successfully.
        Notice: Trust flag u is set automatically if the private key is present.
        Notice: Trust flag u is set automatically if the private key is present.
        Intermediate certificates Imported successfully. 
        
        Saving the required configuration
        config/oe-letsencrypt-client.conf configuration saved in /etc/ipsec.d 
        
        Restarting Ipsec
        Redirecting to: systemctl restart ipsec.service

### For Server

        $ sudo bash setup
        [sudo] password for user:

        Checking if the script is run as root.
        This script is run as root. Good to go. 
        
        Installing for server or client? Type (S/C) s
        Checking if IPsec is installed
        IPsec is installed. 
        
        Downloading the letsencrypt certificates
        Deleting the certs directories certs/CA , certs/intermediate (if previously present)
        CA Certificates downloaded.
        Intermediate Certificates downloaded. 
        
        Initializing the nss database
        NSS database already initialised - aborted
        To wipe the old NSS database, issue: rm /etc/ipsec.d/*.db
        
        Importing the downloaded certificates into NSS Database
        CA certificates Imported successfully.
        Notice: Trust flag u is set automatically if the private key is present.
        Notice: Trust flag u is set automatically if the private key is present.
        Intermediate certificates Imported successfully. 
        
        Saving the required configuration
        config/oe-letsencrypt-server.conf configuration saved in /etc/ipsec.d 
        
        Restarting Ipsec
        Redirecting to: systemctl restart ipsec.service


## Features Implemented so far

1. The script can only be run as root. 

> The script checks if it is run as root or not. It is essential as to make changes in /etc/ipsec.d the script need root privileges.

2. The script checks if IPsec is installed. 

> If not installed, the script exits after showing prompt with various available ways to install IPsec.

3. Script downloads the letsencrypt certificates CA and intermediate certificates. 

> If the script fails to download the certificates then it exits. Showing the error status. The possible reason for its failure was not running the script as `root` but that is fixed now. 


4. Script saves the downloaded certificates in `certs` directory.

> If the script is run once then the certificates are downloaded in the `certs` directory. But if one tries to redo the whole process(i.e. in case the certs are expired.), the old certs are deleted and new ones are downloaded.

5. Script on repeated running (i.e. in case the certs are expired.) replaces the old configuration and certs and with the new updated certs and default configuration.

6. The Script initializes the nssdb if not initialized before.

7. The downloaded CA and intermediate certs are imported in the nssdb.

8. The script adds the server/client configuration to /etc/ipsec.d based on the user preference.

> The user is asked, if he is Installing for server or client?

9. After performing all the above steps, script restarts the ipsec service.